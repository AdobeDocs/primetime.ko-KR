---
description: CustomRangeMetadata 클래스는 VOD 스트림 표시, 삭제 및 바꾸기에서 서로 다른 유형의 시간 범위를 식별합니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.
seo-description: CustomRangeMetadata 클래스는 VOD 스트림 표시, 삭제 및 바꾸기에서 서로 다른 유형의 시간 범위를 식별합니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.
seo-title: 사용자 지정 시간 범위 작업
title: 사용자 지정 시간 범위 작업
uuid: eadd4d8d-0e03-40ca-ae3b-eede82bf2df8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 사용자 지정 시간 범위 작업 {#custom-time-range-operations}

CustomRangeMetadata 클래스는 VOD 스트림에서 서로 다른 유형의 시간 범위를 식별합니다.표시, 삭제 및 바꾸기 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

광고 삭제 및 교체에 대해 TVSDK는 다음과 같은 *사용자 지정 시간 범위 작업* 모드를 사용합니다.

* **표시** 이 모드를 이전 버전의 TVSDK에서 사용자 지정 광고 마커라고 했습니다. 모드는 VOD 스트림에 이미 삽입된 광고의 시작 및 종료 시간을 표시합니다. 스트림에 `MARK` 유형의 시간 범위 마커가 있으면 에 의해 초기 배치가 생성되어 에 의해 `Mode.MARK` `CustomMarkerOpportunityGenerator` `CustomRangeResolver`해결됩니다. 삽입된 광고가 없습니다.

* **삭제** 시간 `DELETE` 범위의 경우, `placementInformation` 유형 초기값이 `Mode.DELETE` 만들어지고 `CustomRangeResolver`이 `DeleteRangeTimelineOperation` 타임라인에서 제거할 범위를 정의하고 TVSDK가 Adobe AVE(Video Engine) API에서 `removeByLocalTime` 이 작업을 완료하는 데 사용합니다. DELETE 범위 및 Adobe Primetime 광고 결정 메타데이터가 있는 경우 해당 범위가 먼저 삭제된 다음, 일반 Adobe Primetime 광고 결정 워크플로우를 사용하여 광고를 `AuditudeResolver` 확인합니다.

* **바꾸기** 시간 `REPLACE` 범위의 경우, 첫 번째 `placementInformations` 는 하나, `Mode.DELETE` `Mode.REPLACE`두 개가 만들어집니다. `CustomRangeResolver` 시간 범위를 먼저 삭제한 다음 지정된 `AuditudeResolver` 광고의 광고를 타임라인에 `replaceDuration` 삽입합니다. 지정하지 `replaceDuration` 않으면 서버에서 삽입할 항목을 결정합니다.

TVSDK는 이러한 사용자 지정 시간 범위 작업을 지원하기 위해 다음을 제공합니다.

* 다양한 컨텐츠 해상도

   스트림에는 광고 신호 모드 및 광고 메타데이터를 기반으로 하는 여러 개의 컨텐츠 해상도가 있을 수 있습니다. 비헤이비어는 다양한 광고 신호 모드 및 광고 메타데이터 조합으로 변경됩니다.
* 다양한 초기 기회를 활용할 수 `CustomMarkerOpportunityGenerator`있습니다.
* 새로운 광고 신호 모드, `CUSTOM_RANGES`.

   광고는 JSON 파일과 같은 외부 소스의 시간 범위 데이터를 기반으로 합니다.