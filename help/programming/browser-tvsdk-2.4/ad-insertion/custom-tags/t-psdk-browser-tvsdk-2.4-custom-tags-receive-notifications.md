---
description: 매니페스트의 태그에 대한 알림을 받으려면 AdobePSDK.TimedMetadataEvent를 수신합니다.
title: 시간 메타데이터 알림에 대한 리스너 추가
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 시간 지정 메타데이터 알림의 리스너 추가{#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 AdobePSDK.TimedMetadataEvent를 수신합니다.

새 `TimedMetadata` 개체가 만들어지면 MediaPlayer는 `AdobePSDK.TimedMetadataEvent`을(를) 전달합니다.

1. 적절한 리스너를 구현합니다.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 이벤트 리스너를 등록합니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3 메타데이터는 동일한 `Events.TimedMetadataEvent`을 통해 전달됩니다. `timedMetadata.type` 속성을 사용하여 TAG와 ID3를 구분할 수 있습니다.

