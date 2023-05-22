---
description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.
title: 사용자 정의 시간 범위 작업
exl-id: 5480b22a-ecff-4fd8-9ec0-40e4a2e97641
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 개요 {#custom-time-range-operations-overview}

TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 콘텐츠의 섹션을 광고 관련 콘텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

광고 삭제 및 대체는 VOD 스트림에서 표시, 삭제 및 바꾸기와 같은 다양한 유형의 시간 범위를 식별하는 사용자 지정 마커로 구현됩니다. 각 사용자 지정 시간 범위에 대해 광고 콘텐츠 삭제 또는 바꾸기를 포함하여 관련 작업을 수행할 수 있습니다.

광고 삭제 및 대체의 경우 TVSDK에는 다음 항목이 포함됩니다 *사용자 정의 시간 범위 작업* 모드:

* 마크 - 디스패치 `AdBreak` 표시된 영역에 대한 이벤트입니다. (이 호출됨 `customAdMarker` 이전 버전의 TVSDK에서) 이 모드에서는 광고 삽입이 허용되지 않습니다.

* DELETE - 이 모드의 경우 앱이 `TimeRangeCollection` 클래스를 사용하여 C3 광고 삭제의 시간 영역을 정의할 수 있습니다. 이 모드에서는 광고 삽입이 허용됩니다.
* 바꾸기 - 이 모드에서 앱은 `timeRange` Adobe Primetime ad decisioning 사용 `AdBreak`. 바꾸기 작업은 C3 광고 삭제가 발생하는 위치에서 시작되고, 표시된 시간(원래 시간 범위보다 짧거나 긴 시간)에 종료됩니다.

TVSDK는 `CustomRangesOpportunityGenerator` 클래스를 사용하여 MARK 및 DELETE 범위에 대한 배치 기회를 생성할 수 있습니다. REPLACE 모드의 경우 TVSDK는 각 시간 범위에 대해 두 개의 배치 기회를 생성합니다.

* 다음 `CustomRangeResolver` DELETE을 위한 배치 기회 생성
* 다음 `AuditudeAdResolver` insert에 대한 배치 기회를 생성합니다.
