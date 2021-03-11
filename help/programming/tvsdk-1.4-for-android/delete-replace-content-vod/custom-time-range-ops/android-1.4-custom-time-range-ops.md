---
description: TVSDK는 VOD 스트림에서 광고 컨텐츠의 프로그래머틱 삭제 및 대체를 지원합니다.
title: 사용자 지정 시간 범위 작업
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# 사용자 지정 시간 범위 작업 {#custom-time-range-operations}

TVSDK는 VOD 스트림에서 광고 컨텐츠의 프로그래머틱 삭제 및 대체를 지원합니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 컨텐츠의 섹션을 광고 관련 컨텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

광고 삭제 및 대체는 VOD 스트림에서 서로 다른 유형의 시간 범위를 식별하는 `TimeRange` 요소로 구현됩니다.표시, 삭제 및 바꾸기 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

광고 삭제 및 대체의 경우 TVSDK는 다음 *사용자 지정 시간 범위 작업* 모드를 사용합니다.

* **MARK**
(이전 버전의 TVSDK에서는 사용자 정의 광고 마커라고 함). 이미 VOD 스트림에 삽입된 광고의 시작 및 종료 시간을 표시합니다. 스트림에 MARK 유형의 시간 범위 마커가 있으면 
`Mode.MARK` 에 의해 생성되고  `CustomAdMarkersContentResolver`해결됩니다. 광고가 삽입되지 않습니다.

* ****
삭제 또는 DELETE 시간 범위, 초기 
`placementInformation` 의 유형 `Mode.DELETE`   `DeleteContentResolver`은 해당 `ContentRemoval` 타임라인에서 제거할 범위를 정의하는 새  `timelineOperation` 기능입니다. TVSDK는 AVE(Adobe 비디오 엔진) API의 `removeByLocalTime`을(를) 사용하여 해당 작업을 용이하게 합니다. DELETE 범위 및 Adobe Primetime 광고 결정(이전에 Auditude라고 함) 메타데이터가 있는 경우, 범위가 먼저 삭제된 후 `AuditudeResolver`은 일반적인 Adobe Primetime 광고 결정 워크플로우를 사용하여 광고를 해결합니다.

* ****
REPLACEEFor REPLACE 시간 범위, 초기 2개 
`placementInformations` 를 만들고  `Mode.DELETE` 하나  `Mode.REPLACE`만듭니다. `DeleteContentResolver`은 시간 범위를 먼저 삭제하고 `AuditudeResolver`는 지정된 `replaceDuration`의 광고를 타임라인에 삽입합니다. `replaceDuration`을(를) 지정하지 않으면 서버에서 삽입할 항목을 결정합니다.

이러한 사용자 지정 시간 범위 작업을 지원하기 위해 TVSDK는 다음을 제공합니다.

* 여러 컨텐츠 해상도

   스트림에는 광고 신호 모드 및 광고 메타데이터를 기반으로 하는 여러 개의 컨텐츠 해상도가 있을 수 있습니다. 비헤이비어는 광고 신호 모드와 광고 메타데이터의 다양한 조합으로 변경됩니다.
* 여러 개의 초기 `PlacementInformations` 광고 신호 모드 및 `MediaPlayerClient`에 의해 해결될 광고 메타데이터를 기준으로 `PlacementInformations` 초기 목록을 만듭니다.`DefaultMediaPlayer`

* 새로운 광고 신호 모드:사용자 지정 시간 범위

   광고는 외부 소스(예: JSON 파일)의 시간 범위 데이터를 기반으로 합니다.