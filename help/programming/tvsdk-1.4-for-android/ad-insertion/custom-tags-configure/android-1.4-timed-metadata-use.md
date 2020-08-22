---
description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
seo-description: 현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.
seo-title: 시간 지정 메타데이터 사용
title: 시간 지정 메타데이터 사용
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# 시간 지정 메타데이터 사용 {#use-timed-metadata}

현재 재생 시간이 시작 시간과 일치하는 경우 TimedMetadata를 사용할 수 있습니다.

재생하는 동안 이러한 저장된 `TimedMetadata` 객체를 사용하려면 Store `ArrayList` 에서 저장된 시간 [의 메타데이터 객체를 전달하면 됩니다](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. 타이머를 실행하고 현재 재생 시간을 반복적으로 쿼리합니다.
1. 현재 재생 시간과 일치하는 시작 시간과 함께 모든 `TimedMetadata` 객체를 찾을 수 있습니다.

   이러한 개체를 사용하여 다양한 작업을 완료할 수 있습니다.

   >[!IMPORTANT]
   >
   >현재 재생 시간이 개체와 일치하는지 여부를 확인할 때 `TimedMetadata` 조건인 `shouldTriggerSubscribedTagEvent` 으로 포함합니다.

   다양한 광고 행동의 결과로 타임라인이 변경될 수 있습니다. 예를 들어 타임라인의 원래 위치에서 하나 이상의 광고 나누기가 이동할 수 있지만, 객체의 시작 시간이 현재 재생 시간과 일치하는지 `shouldTriggerSubscribedTagEvent` `TimeMetadata` 확인합니다.

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

1. 목록에서 오래된 `TimedMetadata` 인스턴스를 정기적으로 플러시하여 메모리가 지속적으로 증가하지 않도록 합니다.