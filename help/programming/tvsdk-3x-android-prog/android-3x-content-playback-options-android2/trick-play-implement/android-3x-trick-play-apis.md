---
description: TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 확인할 수 있는 방법, 속성 및 이벤트가 포함되어 있습니다.
title: 속도 변경 API 요소
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# 속도 변경 API 요소 {#rate-change-api-elements}

TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 확인할 수 있는 방법, 속성 및 이벤트가 포함되어 있습니다.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

다음 API 요소를 사용하여 재생 속도를 변경할 수 있습니다.

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`를 반환합니다.

| **비율 값** | **재생 효과** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 지정된 승수가 정상보다 빠릅니다(예: 4가 정상보다 4배 빠름). |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | 빨리 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환합니다. `play` 호출은 rate 속성을 1.0으로 설정하는 것과 같습니다. |
| 0.0 | 일시 중지(`pause` 호출은 rate 속성을 0.0으로 설정하는 것과 동일) |