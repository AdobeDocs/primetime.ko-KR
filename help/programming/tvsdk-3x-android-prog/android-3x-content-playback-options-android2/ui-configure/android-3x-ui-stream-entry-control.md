---
description: 기본적으로 재생을 시작할 때 VOD 미디어는 0에서 시작되고 라이브 미디어는 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 재정의할 수 있습니다.
title: 특정 시간에 스트림 입력
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 특정 시간에 스트림 입력 {#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작할 때 VOD 미디어는 0에서 시작되고 라이브 미디어는 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 재정의할 수 있습니다.

1. 위치 전달 `MediaPlayer.prepareToPlay`.

   TVSDK는 지정된 위치를 자산의 시작점으로 간주하므로 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 있지 않으면 TVSDK는 기본 위치를 사용합니다. 자세한 내용은 [미디어 플레이어에서 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

   예:

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
