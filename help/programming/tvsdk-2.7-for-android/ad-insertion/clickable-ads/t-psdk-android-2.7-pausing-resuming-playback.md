---
description: 사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.
seo-description: 사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.
seo-title: 재생 일시 중지 및 다시 시작
title: 재생 일시 중지 및 다시 시작
uuid: 229e2499-e30e-458c-bd6d-d035588c21cf
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# 재생 일시 중지 및 다시 시작 {#pause-and-resume-playback}

사용자가 광고를 클릭하면 애플리케이션에서 기본 비디오 컨텐츠의 재생을 일시 중지해야 합니다.

1. Android 활동에서 `onPause` 및 `onResume` 무시

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

