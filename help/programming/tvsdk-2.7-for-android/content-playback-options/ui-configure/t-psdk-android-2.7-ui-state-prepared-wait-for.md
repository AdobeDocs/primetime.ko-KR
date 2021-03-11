---
description: 대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태 대기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 유효한 상태 {#wait-for-a-valid-state}을(를) 기다립니다.

TVSDK를 사용하면 실시간 및 VOD(Video On Demand)를 위한 기본 재생 경험을 제어할 수 있습니다. TVSDK는 플레이어 사용자 인터페이스를 구성하는 데 사용할 수 있는 플레이어 인스턴스에 메서드 및 속성을 제공합니다.

대부분의 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필요한 상태 이상이 아니면 많은 플레이어 메서드에서 `MediaPlayerException`을(를) throw합니다.

필요한 상태는 일반적으로 PREMITED입니다. 이 경우 `StatusChangeEventListener.onStatusChanged()`에 대한 콜백 루틴이 실행됩니다.

1. 상태가 `PREPARED`인지 확인하려면 `MediaPlayer.MediaPlayerStatus`을 선택합니다.
