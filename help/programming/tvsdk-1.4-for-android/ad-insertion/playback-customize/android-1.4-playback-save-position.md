---
description: 비디오의 현재 재생 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 다시 시작할 수 있습니다.
seo-description: 비디오의 현재 재생 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 다시 시작할 수 있습니다.
seo-title: 비디오 위치를 저장하고 나중에 다시 시작합니다.
title: 비디오 위치를 저장하고 나중에 다시 시작합니다.
uuid: 322f780d-09ba-44b0-b2e5-46288bf58fda
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 비디오 위치를 저장하고 나중에 다시 시작합니다. {#save-the-video-position-and-resume-later}

비디오의 현재 재생 위치를 저장하고 이후 세션에서 동일한 위치에서 재생을 다시 시작할 수 있습니다.

동적으로 삽입된 광고는 사용자 세션마다 다르므로 **겹친 광고로 위치를** 저장하는 것은 향후 세션에서 다른 위치를 나타냅니다. TVSDK 파섹

1. 사용자가 비디오를 종료하면 애플리케이션에서 해당 위치를 검색하여 비디오에 저장합니다.

   >[!TIP]
   >
   >광고 기간은 포함되지 않습니다.

   광고 브레이크는 광고 패턴, 빈도 매핑 등으로 인해 각 세션에서 달라질 수 있습니다. 한 세션에서 비디오의 현재 시간은 이후 세션에서 다를 수 있습니다. 비디오의 위치를 저장할 때 응용 프로그램은 로컬 시간을 검색하여 장치 또는 서버의 데이터베이스에 저장할 수 있습니다.

   예를 들어 사용자가 비디오의 20분 지점에 있고 이 위치에 광고 5분이 포함된 경우 1200초를 `getCurrentTime` 반환하고 `getLocalTime` 이 위치에서는 900초를 반환합니다.

   >[!IMPORTANT]
   >
   >실시간/선형 스트림의 경우 로컬 시간과 현재 시간이 동일합니다. 이 경우 아무런 `convertToLocalTime` 효과가 없습니다. VOD의 경우, 광고가 재생되는 동안 현지 시간은 변경되지 않습니다.

   ```java
   // Save the user session when player activity stops 
   @Override 
   public void onStop() { 
       super.onStop(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences( 
                 getActivity().getApplicationContext() 
               ); 
       SharedPreferences.Editor editor = prefs.edit(); 
       // get the local time where stream stopped playing and  
       // save it in System preferences 
       editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
       editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
       editor.commit(); 
       ... 
   } 
   ```

1. 플레이어 활동이 다시 시작되면 사용자 세션을 복원합니다.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil").equals(_contentInfo.toMediaResource().getUrl())) { 
   
           _lastKnownLocalTime = prefs.getLong(LAST_LOCAL_TIME, 0);    // get the last local time saved  
                                                                       // in system preferences 
           if (_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. 동일한 위치에서 비디오를 다시 시작하려면 다음을 수행합니다.

   * 이전 세션에서 저장한 위치에서 비디오 재생을 다시 시작하려면 을 `seekToLocalTime`사용합니다.

      >[!TIP]
      >
      >이 메서드는 로컬 시간 값에서만 호출됩니다. 메서드가 현재 시간 결과와 함께 호출되면 잘못된 동작이 발생합니다.

   * 현재 시간을 검색하려면 을 `seek`사용합니다.

1. 응용 프로그램이 `onStatusChanged` 상태 변경 이벤트를 받으면 저장된 현지 시간으로 이동합니다.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if (_shouldResumePlayback) { 
               if(_lastKnownLocalTime >= 0) { 
                   _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
        ... 
   } 
   ```

1. 광고 정책 인터페이스에 지정된 대로 광고 나누기를 제공합니다.
1. 기본 광고 정책 선택기를 확장하여 사용자 지정 광고 정책 선택기를 구현합니다.
1. 구현하여 사용자에게 제공해야 하는 광고 나누기를 `selectAdBreaksToPlay`제공합니다.

   이 방법에는 프리롤 광고 중단과 로컬 시간 위치 이전의 미드롤 광고 브레이크가 포함됩니다. 애플리케이션에서 프리롤 광고 브레이크를 재생하고 지정된 현지 시간으로 다시 시작하거나, 미드롤 광고 브레이크를 재생하고, 지정된 현지 시간으로 다시 시작하거나, 광고 브레이크를 재생하지 않습니다.
