---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태를 기다립니다.
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 유효한 상태를 기다립니다. {#wait-for-a-valid-state}

TVSDK를 사용하여 라이브 및 VOD(Video On Demand)에 대한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스의 메서드와 속성을 제공합니다.대부분의 TVSDK 플레이어 메서드를 사용하려면 플레이어가 올바른 상태여야 합니다.

플레이어는 다양한 상태를 통해 이동합니다. 플레이어가 올바른 상태가 될 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 적어도 필수 상태가 아니면 많은 플레이어 메서드가 throw를 수행합니다 `IllegalStateException`.

필요한 상태는 일반적으로 준비됩니다.

1. 상태가 준비되었는지 확인하려면:

   플레이어가 초기화될 때 TVSDK가 콜백을 호출할 때까지 기다립니다. `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 준비됨 상태의 이벤트입니다.

   의 현재 상태를 확인하려면 `MediaPlayer` 개체가 적어도 준비되었습니다.

   ```
   function getstatus():String;
   ```
