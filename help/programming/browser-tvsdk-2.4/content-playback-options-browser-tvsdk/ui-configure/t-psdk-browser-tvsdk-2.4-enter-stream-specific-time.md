---
description: 기본적으로 재생이 시작되면 VOD 미디어는 0에서 시작되고 라이브 미디어는 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 재정의할 수 있습니다.
title: 특정 시간에 스트림 입력
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 특정 시간에 스트림 입력{#enter-a-stream-at-a-specific-time}

기본적으로 재생이 시작되면 VOD 미디어는 0에서 시작되고 라이브 미디어는 클라이언트 라이브 포인트(MediaPlayer.LIVE_POINT)에서 시작됩니다. 기본 동작을 재정의할 수 있습니다.

1. 위치 전달 `MediaPlayer.prepareToPlay`.
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
