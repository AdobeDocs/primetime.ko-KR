---
description: 브라우저 TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.
title: 비디오 재생 및 일시 중지
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 비디오 재생 및 일시 중지{#play-and-pause-a-video}

브라우저 TVSDK 비헤이비어를 추가하여 단추를 일시 정지하고 재생할 수 있습니다.

1. 다음을 수행하는 일시 중지/재생 단추를 만듭니다.
   1. 플레이어가 준비 상태가 될 때까지 기다리십시오.
   1. 재생을 시작하려면 브라우저 TVSDK 재생 방법을 호출합니다.

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. 재생을 일시 중지하려면 브라우저 TVSDK 일시 중지 방법을 호출합니다.

      ```java
      void pause() throws IllegalStateException;
      ```

1. `AdobePSDK.MediaPlayerStatusChangeEvent` 이벤트를 수신하여 오류를 확인하거나 다른 적절한 작업을 수행합니다.

   Browser TVSDK는 일시 중지 또는 재생 메서드가 호출될 때 이 이벤트를 트리거하고 `MediaPlayerStatus.PLAYING` 또는 `MediaPlayerStatus.PAUSED` 등의 새 상태를 비롯한 이벤트 개체에 대한 정보를 전달합니다.

