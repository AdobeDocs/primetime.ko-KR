---
description: TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 메서드, 속성 및 이벤트가 포함되어 있습니다.
seo-description: TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 메서드, 속성 및 이벤트가 포함되어 있습니다.
seo-title: 속도 변경 API 요소
title: 속도 변경 API 요소
uuid: 3554bf45-9419-4740-8a0e-484fc14c7436
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 속도 변경 API 요소 {#rate-change-api-elements}

TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 메서드, 속성 및 이벤트가 포함되어 있습니다.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

다음 API 요소를 사용하여 재생 속도를 변경할 수 있습니다.

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`를 지정합니다.

| 비율 값 | 재생에 효과 적용 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 지정된 승수가 보통보다 더 빨리 지정된 상태에서 빨리 감기 모드로 전환합니다(예: 4가 평상시보다 4배 더 빠름). |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 빨리 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환합니다. 호출은 rate 속성을 1.0으로 설정하는 `play` 것과 같습니다. |
| 0.0 | 일시 중지(호출은 rate 속성을 0.0으로 설정하는 `pause` 것과 동일) |

