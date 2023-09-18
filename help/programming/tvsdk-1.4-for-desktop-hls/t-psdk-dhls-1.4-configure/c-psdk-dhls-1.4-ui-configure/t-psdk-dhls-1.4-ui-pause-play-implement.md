---
description: 일시 중지 및 재생 버튼을 위해 TVSDK 동작을 추가할 수 있습니다.
title: 비디오 재생 및 일시 중지
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

일시 중지 및 재생 버튼을 위해 TVSDK 동작을 추가할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 적어도 준비됨 상태가 될 때까지 기다립니다.
   1. 재생을 시작하려면 TVSDK 재생 메서드를 호출합니다.

      ```
      function play():void;
      ```

   1. 재생을 일시 중지하려면 TVSDK 일시 중지 메서드를 호출합니다.

      ```
      function pause():void;
      ```

1. 콜백을 사용합니다. `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 오류를 확인하거나 기타 적절한 작업을 수행하는 이벤트입니다.

   TVSDK는 일시 중지 또는 재생 메서드가 호출될 때 이 콜백을 호출합니다. TVSDK는 일시 중지됨 또는 재생 등의 새 상태를 포함하여 콜백의 상태 변경에 대한 정보를 전달합니다.
