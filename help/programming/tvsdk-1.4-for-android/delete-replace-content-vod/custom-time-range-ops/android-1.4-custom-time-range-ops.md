---
description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.
title: 사용자 정의 시간 범위 작업
exl-id: 10aa3609-d5d0-49e2-959f-d72d8dbd6ef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 사용자 정의 시간 범위 작업 {#custom-time-range-operations}

TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 콘텐츠의 섹션을 광고 관련 콘텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

광고 삭제 및 교체는 `TimeRange` vod 스트림에서 표시, 삭제 및 바꾸기와 같은 다양한 유형의 시간 범위를 식별하는 요소입니다. 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 콘텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

광고 삭제 및 대체의 경우 TVSDK는 다음을 사용합니다 *사용자 정의 시간 범위 작업* 모드:

* **표시**
(이전 버전의 TVSDK에서는 이를 사용자 지정 광고 마커라고 했습니다.) 이미 VOD 스트림에 배치된 광고의 시작 및 종료 시간을 표시합니다. 스트림에 MARK 유형의 시간 범위 마커가 있는 경우 
`Mode.MARK` 이(가) 을(를) 생성하여 해결했습니다. `CustomAdMarkersContentResolver`. 광고가 삽입되지 않습니다.

* **DELETE**
DELETE 시간 범위의 경우, 초기 
`placementInformation` 유형 `Mode.DELETE` 이(가) 해당 사용자에 의해 만들어지고 해결됩니다 `DeleteContentResolver`. `ContentRemoval` 새 항목 `timelineOperation` 타임라인에서 제거할 범위를 정의합니다. TVSDK 사용 `removeByLocalTime` (AVE(Adobe 비디오 엔진) API에서)를 참조하십시오. DELETE 범위와 Adobe Primetime 광고 결정 (이전의 Auditude) 메타데이터가 있는 경우 범위가 먼저 삭제되고 `AuditudeResolver` 는 일반적인 Adobe Primetime ad decisioning 워크플로를 사용하여 광고를 해결합니다.

* **바꾸기**
REPLACE 시간 범위의 경우 두 개의 초기 
`placementInformations` 만들어짐, 하나 `Mode.DELETE` 및 1 `Mode.REPLACE`. 다음 `DeleteContentResolver` 시간 범위를 먼저 삭제한 다음 `AuditudeResolver` 지정된 광고 삽입 `replaceDuration` 타임라인에 삽입하십시오. 없는 경우 `replaceDuration` 을 지정하면 서버에서 삽입할 항목을 결정합니다.

이러한 사용자 지정 시간 범위 작업을 지원하기 위해 TVSDK는 다음을 제공합니다.

* 여러 콘텐츠 해결자

   스트림은 광고 시그널링 모드 및 광고 메타데이터에 기초하여 다수의 콘텐츠 해결기들을 가질 수 있다. 비헤이비어는 광고 시그널링 모드와 광고 메타데이터의 다른 조합으로 변경됩니다.
* 여러 개의 초기 `PlacementInformations` 다음 `DefaultMediaPlayer` 초기 목록 만들기 `PlacementInformations` 에서 확인할 광고 신호 모드 및 광고 메타데이터 기반 `MediaPlayerClient`.

* 새로운 광고 신호 모드: 사용자 지정 시간 범위

   광고는 외부 소스(예: JSON 파일)의 시간 범위 데이터를 기반으로 배치됩니다.
