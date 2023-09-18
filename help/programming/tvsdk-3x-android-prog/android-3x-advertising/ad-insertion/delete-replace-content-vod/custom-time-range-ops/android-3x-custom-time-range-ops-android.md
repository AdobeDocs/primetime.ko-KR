---
description: CustomRangeMetadata 클래스는 VOD 스트림 표시, 삭제 및 바꾸기에서 서로 다른 유형의 시간 범위를 식별합니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 콘텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.
title: 사용자 정의 시간 범위 작업
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 사용자 정의 시간 범위 작업 {#custom-time-range-operations}

CustomRangeMetadata 클래스는 VOD 스트림에서 표시, 삭제 및 바꾸기와 같은 다양한 유형의 시간 범위를 식별합니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 콘텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

광고 삭제 및 대체의 경우 TVSDK는 다음을 사용합니다 *사용자 정의 시간 범위 작업* 모드:

* **표시** 이 모드는 이전 버전의 TVSDK에서 사용자 지정 광고 마커라고 했습니다. 모드는 이미 VOD 스트림에 배치된 광고의 시작 및 종료 시간을 표시합니다. 유형의 시간 범위 표시자가 있는 경우 `MARK` 스트림에서 의 초기 배치 `Mode.MARK` 다음에 의해 생성됨: `CustomMarkerOpportunityGenerator` 해결한 사람: `CustomRangeResolver`. 광고가 삽입되지 않습니다.

* **DELETE** 대상 `DELETE` 시간 범위, 초기 `placementInformation` 유형 `Mode.DELETE` 다음에 의해 만들어지고 해결됨: `CustomRangeResolver`. `DeleteRangeTimelineOperation` 타임라인에서 제거할 범위를 정의하며 TVSDK는 `removeByLocalTime` (AVE(Adobe 비디오 엔진) API에서)로 이동하여 이 작업을 완료합니다. DELETE 범위와 Adobe Primetime 광고 결정 메타데이터가 있는 경우 범위가 먼저 삭제된 다음 `AuditudeResolver` 는 일반적인 Adobe Primetime ad decisioning 워크플로를 사용하여 광고를 해결합니다.

* **바꾸기** 대상 `REPLACE` 시간 범위, 두 개의 초기 `placementInformations` 만들어짐, 하나 `Mode.DELETE` 및 1 `Mode.REPLACE`. `CustomRangeResolver` 시간 범위를 먼저 삭제한 다음 `AuditudeResolver` 지정된 광고 삽입 `replaceDuration` 타임라인에 삽입하십시오. 없는 경우 `replaceDuration` 을 지정하면 서버에서 삽입할 항목을 결정합니다.

이러한 사용자 지정 시간 범위 작업을 지원하기 위해 TVSDK는 다음을 제공합니다.

* 여러 콘텐츠 해결자

  스트림은 광고 시그널링 모드 및 광고 메타데이터에 기초하여 다수의 콘텐츠 해결기들을 가질 수 있다. 비헤이비어는 광고 시그널링 모드와 광고 메타데이터의 다른 조합으로 변경됩니다.
* 을 사용하는 여러 개의 초기 기회 `CustomMarkerOpportunityGenerator`.
* 새로운 광고 신호 모드, `CUSTOM_RANGES`.

  광고는 JSON 파일과 같은 외부 소스의 시간 범위 데이터를 기반으로 배치됩니다.
