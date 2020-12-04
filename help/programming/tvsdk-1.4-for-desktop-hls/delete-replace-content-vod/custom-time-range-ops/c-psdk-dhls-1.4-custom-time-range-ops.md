---
description: TVSDK는 VOD 스트림으로 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 대체하도록 지원합니다.
seo-description: TVSDK는 VOD 스트림으로 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 대체하도록 지원합니다.
seo-title: 사용자 지정 시간 범위 작업
title: 사용자 지정 시간 범위 작업
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 개요 {#custom-time-range-operations-overview}

TVSDK는 VOD 스트림으로 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 대체하도록 지원합니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 컨텐츠의 섹션을 광고 관련 컨텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

광고 삭제 및 대체는 VOD 스트림에서 다양한 유형의 시간 범위를 식별하는 사용자 정의 마커를 사용하여 구현됩니다.표시, 삭제 및 바꾸기 각 사용자 지정 시간 범위에 대해 광고 컨텐츠 삭제 또는 바꾸기를 포함하여 관련 작업을 수행할 수 있습니다.

광고 삭제 및 바꾸기 시 TVSDK에는 다음과 같은 *사용자 지정 시간 범위 작업* 모드가 포함되어 있습니다.

* MARK - 표시된 영역에 대해 `AdBreak` 이벤트를 전달합니다. (이전 버전의 TVSDK에서는 `customAdMarker`이라고 합니다.) 광고 삽입은 이 모드에서 허용되지 않습니다.

* DELETE - 이 모드에서는 앱이 `TimeRangeCollection` 클래스를 사용하여 C3 광고 삭제에 대한 시간 영역을 정의합니다. 광고 삽입은 이 모드에서 허용됩니다.
* REPLACE - 이 모드에서는 앱이 `timeRange`을(를) Adobe Primetime 광고 결정 `AdBreak`으로 대체합니다. 바꾸기 작업은 C3 광고 삭제가 발생하는 곳에서 시작되며 지정된 시간(원래 시간 범위보다 짧거나 긴 시간)에 끝납니다.

TVSDK는 MARK 및 DELETE 범위에 대한 배치 기회를 생성하는 `CustomRangesOpportunityGenerator` 클래스를 제공합니다. REPLACE 모드의 경우 TVSDK는 각 시간 범위에 대해 두 개의 배치 기회를 생성합니다.

* `CustomRangeResolver`은 DELETE에 대한 배치 기회를 생성합니다.
* `AuditudeAdResolver`은 INSERT에 대한 배치 기회를 생성합니다.