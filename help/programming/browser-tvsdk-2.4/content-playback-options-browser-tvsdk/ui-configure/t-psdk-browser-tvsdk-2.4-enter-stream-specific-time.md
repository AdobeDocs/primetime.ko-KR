---
description: 기본적으로 재생이 시작되면 VOD 미디어는 0에서 시작하고 라이브 미디어는 클라이언트 라이브 지점(MediaPlayer.LIVE_POINT)에서 시작합니다. 기본 동작을 재정의할 수 있습니다.
title: 특정 시간에 스트림 입력
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 특정 시간에 스트림 입력{#enter-a-stream-at-a-specific-time}

기본적으로 재생이 시작되면 VOD 미디어는 0에서 시작하고 라이브 미디어는 클라이언트 라이브 지점(MediaPlayer.LIVE_POINT)에서 시작합니다. 기본 동작을 재정의할 수 있습니다.

1. 위치를 `MediaPlayer.prepareToPlay`에 전달합니다.
1. 브라우저 TVSDK는 이 위치를 자산의 시작점으로 사용합니다.

   >[!NOTE]
   >
   >검색 작업이 필요하지 않습니다.

1. 위치가 검색 가능한 범위 내에 없으면 기본 위치가 사용됩니다.

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

