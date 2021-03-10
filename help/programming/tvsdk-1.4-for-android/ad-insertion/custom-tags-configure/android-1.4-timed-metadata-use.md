---
description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
title: 시간 지정 메타데이터 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 시간 메타데이터 {#use-timed-metadata} 사용

현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.

재생하는 동안 이러한 저장된 `TimedMetadata` 개체를 사용하려면 [Store 시간 지정 메타데이터 개체가 전달될 때 `ArrayList`에 저장된 을 사용합니다.](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md)

1. 타이머를 실행하고 현재 재생 시간을 반복적으로 쿼리합니다.
1. 현재 재생 시간과 일치하는 시작 시간이 있는 `TimedMetadata` 개체를 모두 찾습니다.

   이러한 객체를 사용하여 다양한 작업을 완료할 수 있습니다.

   >[!IMPORTANT]
   >
   >현재 재생 시간이 `TimedMetadata` 개체와 일치하는지 여부를 확인할 때는 `shouldTriggerSubscribedTagEvent`을 조건으로 포함합니다.

   다양한 광고 동작의 결과로 타임라인이 변경될 수 있습니다. 예를 들어 하나 이상의 광고 나누기가 타임라인의 원래 위치에서 이동될 수 있지만 `shouldTriggerSubscribedTagEvent`은 `TimeMetadata` 개체의 시작 시간이 현재 재생 시간과 일치하도록 합니다.

   예:

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. 메모리가 지속적으로 증가하지 않도록 목록에서 오래된 `TimedMetadata` 인스턴스를 정기적으로 플러시합니다.