---
description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
seo-title: 사용자 지정 컨텐츠 해결 프로그램 구현
title: 사용자 지정 컨텐츠 해결 프로그램 구현
uuid: cf85dd90-242e-4f9e-9785-158ca0fc9465
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 사용자 지정 컨텐츠 확인자 구현{#implement-a-custom-content-resolver}

기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.

Browser TVSDK가 새로운 기회를 감지하면 등록된 컨텐츠 해상도에서 `canResolve` 메서드를 사용하여 해당 기회를 해결할 수 있는 컨텐츠를 검색합니다. true를 반환한 첫 번째 값이 기회를 해결하기 위해 선택됩니다. 컨텐츠 확인자가 없으면 해당 기회를 건너뜁니다. 컨텐츠 확인 프로세스는 일반적으로 비동기 방식이므로, 컨텐츠 확인자는 프로세스가 완료되면 브라우저 TVSDK에 알릴 책임이 있습니다.

다음 정보를 기억하십시오.

* 컨텐츠 확인자는 `client.process`을(를) 호출하여 TVSDK가 실행해야 하는 타임라인 작업을 지정합니다.

   일반적으로 이 작업은 광고 중단 배치입니다.

* 내용 확인자는 해결 프로세스가 성공한 경우 `client.notifyCompleted`, 프로세스가 실패한 경우 `client.notifyFailed` 을 호출합니다.

1. 사용자 지정 기회 해결 프로그램을 만듭니다.

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

1. 사용자 지정 컨텐츠 확인자를 사용하는 사용자 지정 컨텐츠 팩터리를 만듭니다.

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

1. 재생할 미디어 스트림에 대한 사용자 정의 컨텐츠 팩터리를 등록합니다.

   UI Framework 플레이어에서 다음과 같이 사용자 지정 콘텐츠 팩터리를 지정할 수 있습니다.

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

