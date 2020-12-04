---
description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 구현하십시오.
seo-description: 매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 구현하십시오.
seo-title: 시간 메타데이터 알림용 수신기 추가
title: 시간 메타데이터 알림용 수신기 추가
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 시간 지정 메타데이터 알림의 수신기를 추가합니다 {#add-listeners-for-timed-metadata-notifications}

매니페스트의 태그에 대한 알림을 받으려면 적절한 이벤트 수신기를 구현하십시오.

애플리케이션에 관련 활동을 알리는 다음 이벤트를 수신하여 시간 메타데이터를 모니터링할 수 있습니다.

* `onTimedMetadata`:콘텐츠를 구문 분석하는 동안 고유한 구독 태그가 식별될 때마다 TVSDK는 새  `TimedMetadata` 개체를 준비하고 이 이벤트를 전달합니다.

   개체에는 구독한 태그의 이름, 이 태그가 나타날 재생 중인 로컬 시간 및 기타 데이터가 포함됩니다.

   이벤트 수신

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
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
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

ID3 메타데이터는 동일한 onTimedMetadata 수신기를 사용하여 ID3 태그가 있음을 나타냅니다. 그러나 `TimedMetadata` 개체의 `type` 속성을 사용하여 TAG와 ID3를 구분할 수 있으므로 혼란이 발생하지는 않습니다. ID3 태그에 대한 자세한 내용은 [ID3 태그](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md)를 참조하십시오.
