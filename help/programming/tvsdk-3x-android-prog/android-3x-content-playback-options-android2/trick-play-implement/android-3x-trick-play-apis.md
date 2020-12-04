---
description: TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 방법, 속성 및 이벤트가 포함되어 있습니다.
seo-description: TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 방법, 속성 및 이벤트가 포함되어 있습니다.
seo-title: 속도 변경 API 요소
title: 속도 변경 API 요소
uuid: c2bcd20c-0641-4d75-802c-08098786d572
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---


# 속도 변경 API 요소 {#rate-change-api-elements}

TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 판별하는 방법, 속성 및 이벤트가 포함되어 있습니다.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

다음 API 요소를 사용하여 재생 속도를 변경할 수 있습니다.

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, 즉 유효한 속도를 지정합니다.

| **비율 값** | **재생에 효과 적용** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 지정된 승수가 정상보다 더 빨리 지정된 다음, 빨리 감기 모드로 전환합니다(예: 4가 정상보다 4배 더 빠름). |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | 빨리 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환합니다. `play` 호출은 rate 속성을 1.0으로 설정하는 것과 동일합니다. |
| 0.0 | 일시 중지(`pause` 호출은 rate 속성을 0.0으로 설정하는 것과 동일) |