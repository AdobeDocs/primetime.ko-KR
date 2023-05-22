---
description: 매니페스트의 태그에 대한 알림을 받으려면 AdobePSDK.TimedMetadataEvent를 수신하십시오.
title: 시간 메타데이터 알림에 대한 리스너 추가
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 시간 메타데이터 알림에 대한 리스너 추가{#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 AdobePSDK.TimedMetadataEvent를 수신하십시오.

새로운 경우 `TimedMetadata` 개체가 만들어지면 MediaPlayer가 디스패치됩니다. `AdobePSDK.TimedMetadataEvent`.

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

ID3 메타데이터가 동일한 `Events.TimedMetadataEvent`. 다음을 사용할 수 있습니다. `timedMetadata.type` TAG와 ID3를 구분하는 속성입니다.
