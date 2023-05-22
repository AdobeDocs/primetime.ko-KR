---
description: 기본적으로 재생을 시작할 때 VOD 미디어가 0에 시작됩니다(MediaPlayer.LIVE_POINT). 기본 동작을 재정의할 수 있습니다.
title: 특정 시간에 스트림 입력
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 특정 시간에 스트림 입력 {#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작할 때 VOD 미디어가 0에 시작됩니다(MediaPlayer.LIVE_POINT). 기본 동작을 재정의할 수 있습니다.

1. 위치 전달 `MediaPlayer.prepareToPlay`.

   TVSDK는 지정된 위치를 자산의 시작점으로 간주합니다. 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 있지 않으면 TVSDK는 기본 위치를 사용합니다.

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
