---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-title: 유효한 상태 대기
title: 유효한 상태 대기
uuid: 918ab021-3685-424a-b84e-683da0357724
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 유효한 상태 대기 {#wait-for-a-valid-state}

TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 인스턴스에서 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 메서드 및 속성을 제공합니다.대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어는 다양한 상태로 이동합니다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필수 상태가 아닌 경우 많은 플레이어 메서드가 throw `IllegalStateException`를 던집니다.

필요한 상태는 일반적으로 준비됩니다.

1. 상태가 준비 상태인지 확인하려면 다음을 수행하십시오.

   플레이어가 초기화되면 TVSDK가 준비된 상태의 이벤트에 대한 콜백을 호출할 때까지 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 기다립니다.

   객체의 현재 상태가 적어도 PREPARED인지 여부를 `MediaPlayer` 확인하려면

   ```
   function getstatus():String;
   ```
