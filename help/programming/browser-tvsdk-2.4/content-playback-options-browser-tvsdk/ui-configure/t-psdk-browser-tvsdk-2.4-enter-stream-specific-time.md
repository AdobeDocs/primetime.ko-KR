---
description: 기본적으로 재생이 시작되면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.
seo-description: 기본적으로 재생이 시작되면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.
seo-title: 특정 시간에 스트림 입력
title: 특정 시간에 스트림 입력
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 특정 시간에 스트림 입력{#enter-a-stream-at-a-specific-time}

기본적으로 재생이 시작되면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 무시할 수 있습니다.

1. 위치를 `MediaPlayer.prepareToPlay`에 전달합니다.
1. 브라우저 TVSDK는 이 위치를 자산의 시작점으로 사용합니다.

   >[!NOTE]
   >
   >검색 작업이 필요하지 않습니다.

1. 위치가 검색 가능한 범위 내에 있지 않으면 기본 위치가 사용됩니다.

   예:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

