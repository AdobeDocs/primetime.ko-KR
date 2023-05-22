---
description: 사용자가 광고를 클릭하면 애플리케이션이 기본 비디오 콘텐츠 재생을 일시 중지해야 합니다.
title: 재생 일시 중지 및 다시 시작
exl-id: 06922c80-b5c1-4e0c-872b-9400e07cf613
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 재생 일시 중지 및 다시 시작 {#pause-and-resume-playback}

사용자가 광고를 클릭하면 애플리케이션이 기본 비디오 콘텐츠 재생을 일시 중지해야 합니다.

재정의 `onPause` 및 `onResume` Android 활동에서.

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```
