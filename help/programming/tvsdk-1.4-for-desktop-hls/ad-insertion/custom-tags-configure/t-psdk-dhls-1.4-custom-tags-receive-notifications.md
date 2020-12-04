---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 등록합니다.
seo-description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 등록합니다.
seo-title: 시간 메타데이터 알림용 수신기 추가
title: 시간 메타데이터 알림용 수신기 추가
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 시간 메타데이터 알림의 수신기 추가{#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 등록합니다.

애플리케이션에 관련 활동을 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `MediaPlayerItemEvent.ITEM_CREATED`:개체의 초기 목록을 만든 후  `TimedMetadata` 사용할 수  `MediaPlayerItem` 있습니다.

   이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `MediaPlayerItemEvent.ITEM_UPDATED`:매니페스트/재생 목록이 정기적으로 새로 고쳐지는 라이브/선형 스트림의 경우 업데이트된 재생 목록/매니페스트에 추가 사용자 지정 태그가 나타날 수 있으므로 추가  `TimedMetadata` 개체가 속성에 추가될 수  `MediaPlayerItem.timedMetadata` 있습니다.

   이 이벤트는 이러한 경우 응용 프로그램에 알립니다.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:새  `TimedMetadata` 개체가 생성될 때마다 이 이벤트는 MediaPlayer에 의해 전달됩니다.

   이 이벤트는 초기화 단계 동안 만들어진 `TimedMetadata` 개체에 대해 전달되지 않습니다.

1. 적절한 수신기를 구현합니다.

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

ID3 메타데이터는 동일한 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`을 통해 전달됩니다. 그러나 TimedMetadata 개체의 `type` 속성을 사용하여 TAG와 ID3을 구별할 수 있으므로 혼란이 발생하지는 않습니다. ID3 태그에 대한 자세한 내용은 [ID3 태그](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)를 참조하십시오.