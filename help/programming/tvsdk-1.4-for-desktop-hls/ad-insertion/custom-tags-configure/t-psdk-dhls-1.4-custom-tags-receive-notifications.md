---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.
title: 시간 지정 메타데이터 알림에 대한 리스너 추가
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 시간 지정 메타데이터 알림의 리스너 추가{#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.

응용 프로그램에 관련 활동을 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `MediaPlayerItemEvent.ITEM_CREATED`:객체의 초기 목록 `TimedMetadata` 은 객체를 만든 후 사용할 수  `MediaPlayerItem` 있습니다.

   이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `MediaPlayerItemEvent.ITEM_UPDATED`:매니페스트/재생 목록이 정기적으로 새로 고쳐지는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 속성에 추가  `TimedMetadata` 객체를 추가할 수  `MediaPlayerItem.timedMetadata` 있습니다.

   이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:새  `TimedMetadata` 객체를 만들 때마다 이 이벤트가 MediaPlayer에 의해 전달됩니다.

   이 이벤트는 초기화 단계 동안 만들어진 `TimedMetadata` 객체에 대해 전달되지 않습니다.

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

ID3 메타데이터는 동일한 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`을 통해 전달됩니다. 그러나 TimedMetadata 객체의 `type` 속성을 사용하여 TAG와 ID3를 구분할 수 있으므로 혼란이 발생하지 않습니다. ID3 태그에 대한 자세한 내용은 [ID3 태그](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)를 참조하십시오.