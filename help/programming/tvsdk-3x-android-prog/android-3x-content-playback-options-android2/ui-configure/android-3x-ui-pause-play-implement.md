---
description: 일시 정지 및 재생 단추를 추가하여 비디오를 일시 정지하거나 재생할 수 있습니다.
seo-description: 일시 정지 및 재생 단추를 추가하여 비디오를 일시 정지하거나 재생할 수 있습니다.
seo-title: 비디오 재생 및 일시 중지
title: 비디오 재생 및 일시 중지
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 비디오 재생 및 일시 중지 {#play-and-pause-a-video}

일시 정지 및 재생 단추를 추가하여 비디오를 일시 정지하거나 재생할 수 있습니다.

1. 일시 정지 또는 재생 단추를 만들려면:
   1. 플레이어가 적어도 준비된 상태가 될 때까지 기다립니다.
   1. 재생을 시작하려면 `play` 메서드를 호출합니다.

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 재생을 일시 중지하려면 `pause()` 메서드를 호출합니다.

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 상태 변경 이벤트 콜백을 사용하여 오류를 확인하거나 다른 적절한 작업을 수행합니다.

   TVSDK는 이 콜백을 `pause()` 호출하거나 `play()` 수신하고 일시 중지되거나 재생되는 등의 새로운 상태를 포함하여 상태 변경에 대한 정보를 전달합니다.