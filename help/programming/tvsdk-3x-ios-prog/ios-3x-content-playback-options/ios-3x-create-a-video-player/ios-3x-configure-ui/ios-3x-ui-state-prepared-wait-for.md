---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태를 기다립니다.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 유효한 상태를 기다립니다. {#wait-for-a-valid-state}

대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어는 다양한 상태를 통해 이동합니다. 플레이어가 올바른 상태가 될 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 적어도 필수 상태가 아니면 많은 플레이어 메서드가 throw를 수행합니다 `IllegalStateException`.

필요한 상태는 일반적으로 입니다. `PTMediaPlayerStatusReady`.
