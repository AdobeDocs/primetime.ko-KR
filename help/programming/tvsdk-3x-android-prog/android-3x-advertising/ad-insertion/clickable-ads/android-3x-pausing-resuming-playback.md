---
description: 사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.
seo-description: 사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.
seo-title: 재생 일시 중지 및 다시 시작
title: 재생 일시 중지 및 다시 시작
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 재생 일시 중지 및 다시 시작 {#pause-and-resume-playback}

사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.

1. Android `onPause` 활동에서 및 `onResume` 을 무시합니다.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

