---
description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작됩니다(MediaPlayer.LIVE_POINT). 기본 동작을 무시할 수 있습니다.
seo-description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작됩니다(MediaPlayer.LIVE_POINT). 기본 동작을 무시할 수 있습니다.
seo-title: 특정 시간에 스트림 입력
title: 특정 시간에 스트림 입력
uuid: ac3479e2-46a1-4ac8-a9e8-68a23f5dd74d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 특정 시간에 스트림 입력 {#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작됩니다(MediaPlayer.LIVE_POINT). 기본 동작을 무시할 수 있습니다.

1. 위치를 `MediaPlayer.prepareToPlay`에 전달합니다.

   TVSDK는 주어진 위치를 자산의 시작점으로 간주합니다. 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 없으면 TVSDK에서 기본 위치를 사용합니다.

   예:

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```

