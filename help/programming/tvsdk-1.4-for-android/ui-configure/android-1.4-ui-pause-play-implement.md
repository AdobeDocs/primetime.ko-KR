---
description: TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.
title: 비디오 재생 및 일시 중지
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 준비 상태가 될 때까지 기다리십시오.
   1. 재생을 시작하려면 TVSDK 재생 메서드를 호출합니다.

      ```java
      void play() throws IllegalStateException;
      ```

   1. 재생을 일시 중지하려면 TVSDK 일시 중지 방법을 호출합니다.

      ```java
      void pause() throws IllegalStateException;
      ```

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 콜백을 사용하여 오류를 확인하거나 다른 적절한 작업을 수행합니다.

   일시 정지 또는 재생 메서드가 호출되면 TVSDK에서 이 콜백을 호출합니다. TVSDK는 PAUSED 또는 PLAYING과 같은 새로운 상태를 포함하여 콜백의 상태 변경에 대한 정보를 전달합니다.

