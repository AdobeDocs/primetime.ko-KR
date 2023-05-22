---
description: 일시 중지 및 재생 버튼을 추가하여 비디오를 일시 중지하거나 재생할 수 있습니다.
title: 비디오 재생 및 일시 중지
exl-id: 7084ef55-4da6-48af-9951-5360bad7bfa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 비디오 재생 및 일시 중지 {#play-and-pause-a-video}

일시 중지 및 재생 버튼을 추가하여 비디오를 일시 중지하거나 재생할 수 있습니다.

1. 일시 중지 또는 재생 단추를 만들려면 다음 작업을 수행하십시오.
   1. 플레이어가 적어도 준비된 상태가 될 때까지 기다립니다.
   1. 재생을 시작하려면 를 호출합니다 `play` 방법:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. 재생을 일시 중지하려면 `pause()` 방법:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. 상태 변경 이벤트 콜백을 사용하여 오류를 확인하거나 기타 적절한 작업을 수행합니다.

   TVSDK가에 대해 이 콜백을 호출합니다. `pause()` 또는 `play()` 일시 중지됨 또는 재생 등 새 상태를 포함하여 상태 변경에 대한 정보를 전달합니다.
