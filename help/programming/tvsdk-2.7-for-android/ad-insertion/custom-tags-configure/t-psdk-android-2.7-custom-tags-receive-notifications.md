---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.
title: 시간 초과된 메타데이터 알림에 대한 리스너 추가
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 시간 초과된 메타데이터 알림에 대한 리스너 추가 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.

다음을 수신하여 시간 초과된 메타데이터를 모니터링할 수 있습니다. `onTimedMetadata`애플리케이션에 관련 활동을 알리는 . 콘텐츠의 구문 분석 중에 고유한 구독 태그가 식별될 때마다 TVSDK는 새 태그를 준비합니다 `TimedMetadata` 및 가 이 이벤트를 전달합니다. 개체에는 구독한 태그의 이름, 이 태그가 표시되는 재생 내 현지 시간 및 기타 데이터가 포함되어 있습니다.

1. 이벤트 수신.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

ID3 메타데이터는 동일한 `onTimedMetadata` listener를 사용하여 ID3 태그가 있는지 확인합니다. 그러나 를 사용할 수 있으므로 혼동을 일으키지 않아야 합니다. `TimedMetadata` `type` TAG와 ID3을 구분하는 속성입니다. ID3 태그에 대한 자세한 내용은  [ID3 태그](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).
