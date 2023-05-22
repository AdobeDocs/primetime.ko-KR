---
description: 대부분의 브라우저 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태를 기다립니다.
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# 유효한 상태를 기다립니다. {#wait-for-a-valid-state}

대부분의 브라우저 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어는 다양한 상태를 통해 이동합니다. 플레이어가 올바른 상태가 될 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 적어도 필수 상태가 아니면 많은 플레이어 메서드가 throw를 수행합니다 `IllegalStateException`.

필요한 상태는 일반적으로 준비됩니다.

1. 상태가 준비되었는지 확인하려면:

   플레이어를 초기화할 때 브라우저 TVSDK가 다음을 디스패치할 때까지 기다립니다. `AdobePSDK.MediaPlayerStatusChangeEvent` 이 있는 이벤트 `event.status` / `MediaPlayerStatus.PREPARED`.

   MediaPlayer 개체의 현재 상태가 PREPARED 이상인지 확인합니다.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
