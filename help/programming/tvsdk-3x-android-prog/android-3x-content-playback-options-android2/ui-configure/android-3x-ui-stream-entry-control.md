---
description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.
seo-description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.
seo-title: 특정 시간에 스트림 입력
title: 특정 시간에 스트림 입력
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# 특정 시간에 스트림 입력 {#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.

1. 위치를 `MediaPlayer.prepareToPlay`에 전달합니다.

   TVSDK는 주어진 위치를 자산의 시작점으로 간주하며 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 없으면 TVSDK에서 기본 위치를 사용합니다. 자세한 내용은 미디어 플레이어[에서 미디어 리소스 로드를 참조하십시오.](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)

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
