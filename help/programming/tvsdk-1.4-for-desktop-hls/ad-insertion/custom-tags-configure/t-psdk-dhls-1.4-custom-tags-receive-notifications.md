---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록하십시오.
title: 시간 초과된 메타데이터 알림에 대한 리스너 추가
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 시간 초과된 메타데이터 알림에 대한 리스너 추가{#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록하십시오.

관련 활동을 애플리케이션에 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `MediaPlayerItemEvent.ITEM_CREATED`: 의 초기 목록 `TimedMetadata` 객체는 다음 이후에서 사용할 수 있습니다. `MediaPlayerItem` 이(가) 만들어졌습니다.

  이 이벤트는 이러한 상황이 발생하면 애플리케이션에 알립니다.

* `MediaPlayerItemEvent.ITEM_UPDATED`: 매니페스트/재생 목록이 주기적으로 새로 고치는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 추가 `TimedMetadata` 개체가 `MediaPlayerItem.timedMetadata` 속성.

  이 이벤트는 이러한 상황이 발생하면 애플리케이션에 알립니다.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: 매번 새로 만들기 `TimedMetadata` 개체가 만들어지고 MediaPlayer에서 이 이벤트를 전달합니다.

  이 이벤트는 다음에 대해 발송되지 않습니다. `TimedMetadata` 초기화 단계에서 생성된 객체입니다.

1. 적절한 리스너를 구현합니다.

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. 이벤트 리스너를 등록합니다.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3 메타데이터가 동일한 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. 그러나 TimedMetadata objtec의 `type` TAG와 ID3을 구분하는 속성입니다. ID3 태그에 대한 자세한 내용은 [ID3 태그](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
