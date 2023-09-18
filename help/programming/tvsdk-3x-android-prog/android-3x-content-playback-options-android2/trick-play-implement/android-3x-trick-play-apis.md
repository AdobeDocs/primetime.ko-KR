---
description: TVSDK에는 유효한 비율, 현재 비율, 트릭 플레이 지원 여부 및 앞으로 감기 및 되감기와 관련된 기타 기능을 결정하는 메서드, 속성 및 이벤트가 포함되어 있습니다.
title: 속도 변경 API 요소
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 속도 변경 API 요소 {#rate-change-api-elements}

TVSDK에는 유효한 비율, 현재 비율, 트릭 플레이 지원 여부 및 앞으로 감기 및 되감기와 관련된 기타 기능을 결정하는 메서드, 속성 및 이벤트가 포함되어 있습니다.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

다음 API 요소를 사용하여 재생 속도를 변경합니다.

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`- 유효한 비율을 지정합니다.

| **비율 값** | **재생에 미치는 영향** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 지정된 승수가 보통보다 빠르게(예: 4가 보통보다 4배 빠름) 빨리 감기 모드로 전환합니다. |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 빠른 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환(호출) `play` rate 속성을 1.0으로 설정하는 것과 같습니다.) |
| 0.0 | 일시 중지(호출) `pause` rate 속성을 0.0으로 설정하는 것과 같습니다.) |
