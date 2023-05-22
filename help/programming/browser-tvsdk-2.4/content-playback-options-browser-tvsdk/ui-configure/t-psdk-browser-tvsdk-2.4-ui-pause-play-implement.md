---
description: 브라우저 TVSDK 동작을 추가하여 버튼을 일시 중지하고 재생할 수 있습니다.
title: 비디오 재생 및 일시 중지
exl-id: ce3f8b0c-9765-4e77-b096-6b9789608fa8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

브라우저 TVSDK 동작을 추가하여 버튼을 일시 중지하고 재생할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 적어도 PREPARED 상태가 될 때까지 기다립니다.
   1. 재생을 시작하려면 브라우저 TVSDK 재생 메서드를 호출합니다.

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 재생을 일시 중지하려면 브라우저 TVSDK 일시 중지 메서드를 호출합니다.

      ```java
      void pause() throws IllegalStateException;
      ```

1. 다음을 들어보십시오. `AdobePSDK.MediaPlayerStatusChangeEvent` 오류를 확인하거나 기타 적절한 작업을 수행하는 이벤트입니다.

   일시 중지 또는 재생 메서드가 호출될 때 브라우저 TVSDK가 이 이벤트를 트리거하고 다음과 같은 새 상태를 포함하여 이벤트 개체에 대한 정보를 전달합니다. `MediaPlayerStatus.PLAYING` 또는 `MediaPlayerStatus.PAUSED`.
