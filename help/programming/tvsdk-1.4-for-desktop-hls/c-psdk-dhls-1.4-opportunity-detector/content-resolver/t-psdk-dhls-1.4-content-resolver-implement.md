---
description: 기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.
title: 사용자 지정 컨텐츠 해결 프로그램 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# 사용자 지정 내용 확인자 구현{#implement-a-custom-content-resolver}

기본 해상도에 따라 고유한 컨텐츠 해상도를 구현할 수 있습니다.

TVSDK가 새로운 기회를 감지하면 등록된 컨텐츠 확인기를 통해 `canResolve` 방법을 사용하여 해당 기회를 해결할 수 있는 기회를 찾습니다. true를 반환한 첫 번째 값이 기회를 해결하기 위해 선택됩니다. 컨텐츠 해결 프로그램을 사용할 수 없는 경우 해당 기회를 건너뜁니다. 컨텐츠 확인 프로세스는 일반적으로 비동기적이므로, 컨텐츠 확인자는 프로세스가 완료되면 TVSDK에 알릴 책임이 있습니다.

* 컨텐츠 확인자는 `client.place`을(를) 호출하여 TVSDK가 실행해야 할 타임라인 작업(일반적으로 광고 중단 배치)을 지정합니다.
* 내용 확인자는 확인 프로세스가 성공한 경우 `client.notifyCompleted`, 프로세스가 실패한 경우 `client.notifyFailed` 을 호출합니다.

1. 사용자 지정 기회 해결 프로그램을 만듭니다.

   ```
   public class CustomResolver extends ContentResolver { 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomResolver() { 
       } 
   
       override protected function doConfigure(item:MediaPlayerItem):void { 
           // here you can read any media stream characteristics which 
           // might help configure your content resolver like 
           // - the media player item configuration through the item.config 
           // - the media resource metadata through item.resource.metadata 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doCanResolve(opportunity:Opportunity):Boolean { 
           // check if the opportunity can be resolved by this resolver 
           // if yes return true, otherwise return false 
   
           return true; 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doResolve(opportunity:Opportunity):void { 
           // start the resolving process 
           // communicate with your custom ad server 
   
           // in this example we assume that: 
           // - if successful, onResolveCompleted method will be invoked 
           // - if failed, onResolveFailed method will be invoked 
       } 
   
       private function onResolveCompleted(response:*):void { 
           try { 
               var proposals:Vector.<TimelineOperation> = new Vector.<TimelineOperation>(); 
   
               // extract the timeline ad placement from the response 
               // and add them to the proposal vector 
               // - extract the ad break 
               // - calculate the placement ( can reuse the opportunity.placement ) 
               // var timelineOperation:AdBreakPlacement = new AdBreakPlacement(placement, adBreak); 
               // proposals.push(timelineOperation); 
   
               client.process(proposals); 
               client.notifyCompleted(_opportunity); 
           } catch (error:Error) { 
               onResolveFailed(error); 
           } 
       } 
   
       private function onResolveFailed(error:Error):void { 
   
           var errorMetadata:Metadata = new Metadata(); 
           MetadataUtils.serializeError(error, errorMetadata); 
   
           var mediaError:MediaError = new MediaError(NotificationCode.CONTENT_RESOLVING_ERROR, errorMetadata); 
           client.notifyFailed(_opportunity, mediaError); 
       } 
   
       ... 
   }
   ```

1. 사용자 지정 컨텐츠 해결 프로그램을 사용하는 사용자 지정 컨텐츠 팩토리를 만듭니다.

   예:

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
           ... 
   
           /** 
            * @inheritDoc 
            */ 
           override protected function  
             doRetrieveResolvers(item:MediaPlayerItem):Vector.<ContentResolver> { 
               var result:Vector.<ContentResolver> = new Vector.<ContentResolver>(); 
   
               var resource:MediaResource = item.resource; 
   
               if (resource.metadata != null) { 
                   if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
                       result.push(new AuditudeAdResolver()); 
                   } else if (resource.metadata.containsKey("custom-opportunity-detector")) { 
                       result.push(new CustomResolver()); 
                   } 
               } 
               return result; 
           } 
   }
   ```

1. 재생할 미디어 스트림에 대한 사용자 정의 컨텐츠 팩토리를 등록합니다.

   예:

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   var advertisingMetadata:AdvertisingMetadata = new AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue("customparam", "customvalue"); 
   
   var metadata:Metadata = new Metadata(); 
   metadata.setMetadata("custom-opportunity-detector", advertisingMetadata); 
   var mediaResource:MediaResource = MediaResource.createFromUrl(url, metadata);
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

