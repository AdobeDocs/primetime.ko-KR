---
description: TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.
seo-description: TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.
seo-title: 비디오 재생 및 일시 중지
title: 비디오 재생 및 일시 중지
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 준비 상태 이상 될 때까지 기다립니다.
   1. 재생을 시작하려면 TVSDK 재생 방법을 호출합니다.

      ```java
      void play() throws IllegalStateException;
      ```

   1. 재생을 일시 중지하려면 TVSDK 일시 중지 방법을 호출합니다.

      ```java
      void pause() throws IllegalStateException;
      ```

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 콜백을 사용하여 오류를 확인하거나 다른 적절한 작업을 수행합니다.

   일시 정지 또는 재생 메서드가 호출되면 TVSDK에서 이 콜백을 호출합니다. TVSDK는 PAUSED 또는 PLAYING과 같은 새로운 상태를 포함하여 콜백에서의 상태 변경에 대한 정보를 전달합니다.

