---
description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
title: 시간 메타데이터 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 시간 메타데이터 사용 {#use-timed-metadata}

현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.

저장된 값을 사용하려면 `TimedMetadata` 재생 중 개체, 저장된 개체 사용 `ArrayList` 출처: [시간 초과된 메타데이터 개체가 디스패치될 때 저장](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. 타이머를 실행하고 현재 재생 시간을 반복적으로 쿼리합니다.
1. 다음 항목 모두 찾기 `TimedMetadata` 시작 시간이 현재 재생 시간과 일치하는 오브젝트.

   이러한 개체를 사용하여 다양한 작업을 완료할 수 있습니다.

   >[!IMPORTANT]
   >
   >현재 재생 시간과 일치하는지 여부를 확인할 때 `TimedMetadata` 개체, 포함 `shouldTriggerSubscribedTagEvent` 조건.

   다양한 광고 동작으로 인해 타임라인이 변경될 수 있습니다. 예를 들어 하나 이상의 광고 브레이크를 타임라인의 원래 위치에서 이동할 수 있지만 `shouldTriggerSubscribedTagEvent` 은(는) 다음을 확인합니다. `TimeMetadata` 오브젝트의 시작 시간은 현재 재생 시간과 일치합니다.

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

1. 부실 주기적으로 플러시 `TimedMetadata` 메모리가 계속 증가하지 않도록 하기 위한 목록의 인스턴스입니다.
