---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
seo-title: 유효한 상태 대기
title: 유효한 상태 대기
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 유효한 상태 대기 {#wait-for-a-valid-state}

TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 환경을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스에 대한 메서드 및 속성을 제공합니다.

대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필요한 상태 이상이 아닌 경우 많은 플레이어 메서드가 `MediaPlayerException`실행됩니다.

필요한 상태는 일반적으로 준비됩니다. 이 경우, 에 대한 콜백 루틴이 `StatusChangeEventListener.onStatusChanged()` 실행됩니다.

1. 상태를 확인하려면 `PREPARED`을 `MediaPlayer.MediaPlayerStatus`확인하십시오.
