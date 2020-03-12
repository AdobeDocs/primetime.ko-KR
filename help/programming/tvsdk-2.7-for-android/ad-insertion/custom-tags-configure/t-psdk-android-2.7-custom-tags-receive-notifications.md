---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.
seo-description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.
seo-title: 시간 메타데이터 알림에 대한 리스너 추가
title: 시간 메타데이터 알림에 대한 리스너 추가
uuid: 336882e7-e2d8-49b8-a23d-f236c7e6a594
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 시간 메타데이터 알림에 대한 리스너 추가 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 리스너를 구현해야 합니다.

에 대한 의견 수렴을 통해 시간 지정 메타데이터를 모니터링할 수 `onTimedMetadata`있으며, 이렇게 하면 애플리케이션에서 관련 활동을 알릴 수 있습니다. 콘텐츠를 구문 분석하는 동안 고유 구독 태그가 식별될 때마다 TVSDK는 새 `TimedMetadata` 개체를 준비하고 이 이벤트를 전달합니다. 개체에는 구독한 태그의 이름, 이 태그가 나타날 재생 중인 로컬 시간 및 기타 데이터가 포함됩니다.

1. 이벤트 수신

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

ID3 메타데이터는 동일한 `onTimedMetadata` 수신기를 사용하여 ID3 태그가 있음을 나타냅니다. 그러나 이 속성을 사용하여 TAG와 ID3를 구별할 수 있으므로 혼동을 일으키지 않아야 합니다. `TimedMetadata` `type` ID3 태그에 대한 자세한 내용은 ID3 [태그를](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md)참조하십시오.