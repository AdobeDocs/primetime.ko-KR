---
description: 기본 확인자를 기반으로 자체 콘텐츠 확인자를 구현할 수 있습니다.
title: 사용자 지정 콘텐츠 확인자 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 사용자 지정 콘텐츠 확인자 구현{#implement-a-custom-content-resolver}

기본 확인자를 기반으로 자체 콘텐츠 확인자를 구현할 수 있습니다.

브라우저 TVSDK가 새 기회를 감지하면 등록된 콘텐츠 해결사를 통해 다음을 사용하여 해당 기회를 해결할 수 있는 기회를 찾습니다. `canResolve` 메서드를 사용합니다. True를 반환하는 첫 번째 항목이 기회 해결을 위해 선택됩니다. 콘텐츠 해결자를 사용할 수 없는 경우 해당 기회를 건너뜁니다. 콘텐츠 해결 프로세스는 일반적으로 비동기적이므로 프로세스가 완료되면 콘텐츠 해결자가 브라우저 TVSDK에 알릴 책임이 있습니다.

다음 정보를 숙지하십시오.

* 콘텐츠 해결자 호출 `client.process` tvsdk에서 실행해야 하는 타임라인 작업을 지정합니다.

  작업은 일반적으로 광고 브레이크 배치입니다.

* 콘텐츠 해결자 호출 `client.notifyCompleted` 해결 프로세스가 성공하거나 `client.notifyFailed` 프로세스가 실패하는 경우

1. 사용자 지정 영업 기회 확인자를 만듭니다.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. 사용자 지정 콘텐츠 확인자를 사용하는 사용자 지정 콘텐츠 팩토리를 만듭니다.

   예:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. 재생할 미디어 스트림에 대한 사용자 지정 콘텐츠 팩토리를 등록합니다.

   UI 프레임워크 플레이어에서 다음과 같이 사용자 지정 콘텐츠 팩토리를 지정할 수 있습니다.

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```
