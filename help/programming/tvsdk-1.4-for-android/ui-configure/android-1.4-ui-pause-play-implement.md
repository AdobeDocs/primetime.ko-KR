---
description: 일시 중지 및 재생 버튼을 위해 TVSDK 동작을 추가할 수 있습니다.
title: 비디오 재생 및 일시 중지
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

일시 중지 및 재생 버튼을 위해 TVSDK 동작을 추가할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 적어도 PREPARED 상태가 될 때까지 기다립니다.
   1. 재생을 시작하려면 TVSDK 재생 메서드를 호출합니다.

      ```java
      void play() throws IllegalStateException;
      ```

   1. 재생을 일시 중지하려면 TVSDK 일시 중지 메서드를 호출합니다.

      ```java
      void pause() throws IllegalStateException;
      ```

1. 사용 `MediaPlayer.PlaybackEventListener.onStateChanged` 오류를 확인하거나 기타 적절한 작업을 수행하기 위한 콜백입니다.

   TVSDK는 일시 중지 또는 재생 메서드가 호출될 때 이 콜백을 호출합니다. TVSDK는 일시 정지됨 또는 재생 과 같은 새 상태를 포함하여 콜백의 상태 변경에 대한 정보를 전달합니다.
