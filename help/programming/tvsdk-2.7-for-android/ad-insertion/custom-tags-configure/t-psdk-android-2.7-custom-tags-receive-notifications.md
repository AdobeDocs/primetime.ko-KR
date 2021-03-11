---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.
title: 시간 지정 메타데이터 알림에 대한 리스너 추가
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 시간 지정 메타데이터 알림에 대한 리스너 추가 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.

응용 프로그램에 관련 활동을 알리는 `onTimedMetadata`을 수신하여 시간 지정 메타데이터를 모니터링할 수 있습니다. 콘텐츠를 구문 분석하는 동안 고유한 구독 태그가 식별될 때마다 TVSDK는 새 `TimedMetadata` 개체를 준비하고 이 이벤트를 전달합니다. 객체에는 가입한 태그의 이름, 이 태그가 나타날 재생 시의 로컬 시간 및 기타 데이터가 포함됩니다.

1. 이벤트를 수신합니다.

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

ID3 메타데이터는 동일한 `onTimedMetadata` 리스너를 사용하여 ID3 태그가 있음을 나타냅니다. 그러나 `TimedMetadata` `type` 속성을 사용하여 TAG와 ID3를 구분할 수 있으므로 혼란이 발생하지 않아야 합니다. ID3 태그에 대한 자세한 내용은 [ID3 태그](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md)를 참조하십시오.