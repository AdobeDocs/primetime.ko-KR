---
description: CustomRangeMetadata 클래스는 VOD 스트림 표시, 삭제 및 바꾸기에서 서로 다른 유형의 시간 범위를 식별합니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.
title: 사용자 지정 시간 범위 작업
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 사용자 지정 시간 범위 작업 {#custom-time-range-operations}

CustomRangeMetadata 클래스는 VOD 스트림에서 서로 다른 유형의 시간 범위를 식별합니다.표시, 삭제 및 바꾸기 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

광고 삭제 및 대체의 경우 TVSDK는 다음 *사용자 지정 시간 범위 작업* 모드를 사용합니다.

* **마켓트** 이 모드는 이전 버전의 TVSDK에서 사용자 지정 광고 마커라고 불렀습니다. 이 모드는 이미 VOD 스트림에 삽입된 광고의 시작 및 종료 시간을 표시합니다. 스트림에 `MARK` 유형의 시간 범위 마커가 있는 경우 `Mode.MARK`의 초기 배치는 `CustomMarkerOpportunityGenerator`에 의해 생성되며 `CustomRangeResolver`에 의해 해결됩니다. 광고가 삽입되지 않습니다.

* **** 삭제 또는  `DELETE` 시간 범위 `placementInformation` 는 유형 `Mode.DELETE` 의 초기 `CustomRangeResolver`를 만들고 이를 통해 확인합니다. `DeleteRangeTimelineOperation` 타임라인에서 제거할 범위를 정의하며, TVSDK는 Adobe AVE(Video Engine) API `removeByLocalTime` 에서 이 작업을 완료하기 위해 사용합니다. DELETE 범위 및 Adobe Primetime 광고 결정 메타데이터가 있는 경우 먼저 범위가 삭제된 다음 `AuditudeResolver`은 일반적인 Adobe Primetime 광고 결정 워크플로우를 사용하여 광고를 해결합니다.

* **대체** 또는  `REPLACE` 시간 범위 `placementInformations` 에 1과 1의  `Mode.DELETE` 초기 두 개 `Mode.REPLACE`가 만들어집니다. `CustomRangeResolver` 시간 범위를 먼저 삭제하고 지정된  `AuditudeResolver` 광고의 광고를 타임라인에  `replaceDuration` 삽입합니다. `replaceDuration`을(를) 지정하지 않으면 서버에서 삽입할 항목을 결정합니다.

이러한 사용자 지정 시간 범위 작업을 지원하기 위해 TVSDK는 다음을 제공합니다.

* 여러 컨텐츠 해상도

   스트림에는 광고 신호 모드 및 광고 메타데이터를 기반으로 하는 여러 개의 컨텐츠 해상도가 있을 수 있습니다. 비헤이비어는 광고 신호 모드와 광고 메타데이터의 다양한 조합으로 변경됩니다.
* `CustomMarkerOpportunityGenerator`을(를) 사용하는 여러 개의 초기 기회.
* 새 광고 신호 모드인 `CUSTOM_RANGES`입니다.

   광고는 JSON 파일과 같은 외부 소스의 시간 범위 데이터를 기반으로 합니다.