---
description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.
seo-description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.
seo-title: 사용자 지정 시간 범위 작업
title: 사용자 지정 시간 범위 작업
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 사용자 지정 시간 범위 작업 {#custom-time-range-operations}

TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 컨텐츠의 섹션을 광고 관련 컨텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

광고 삭제 및 대체는 VOD 스트림에서 서로 다른 유형의 시간 범위를 식별하는 `TimeRange` 요소로 구현됩니다.표시, 삭제 및 바꾸기 이러한 각 사용자 지정 시간 범위 유형에 대해 광고 컨텐츠 삭제 및 바꾸기를 포함하여 해당 작업을 수행할 수 있습니다.

광고 삭제 및 교체에 대해 TVSDK는 다음과 같은 *사용자 지정 시간 범위 작업* 모드를 사용합니다.

* **MARK**(이전 버전의 TVSDK에서는 사용자 지정 광고 마커라고 함). VOD 스트림에 이미 삽입된 광고의 시작 시간과 종료 시간을 표시합니다. 스트림에 MARK 유형의 시간 범위 마커가 있으면 에 의해 초기 배치가 `Mode.MARK` 생성되고 해결됩니다 `CustomAdMarkersContentResolver`. 삽입된 광고가 없습니다.

* **DELETE** DELETE 시간 범위의 경우, `placementInformation` 해당 유형에 의해 초기 유형이 `Mode.DELETE` 만들어지고 해결됩니다 `DeleteContentResolver`. `ContentRemoval` 는 타임라인에서 제거할 범위를 정의하는 새로운 `timelineOperation` 기능입니다. TVSDK는 Adobe AVE(Video Engine) API를 `removeByLocalTime` 사용하여 작업을 용이하게 합니다. DELETE 범위 및 Adobe Primetime 광고 결정(이전의 Auditude) 메타데이터가 있는 경우, 범위가 먼저 삭제된 다음, 일반 Adobe Primetime 광고 결정 워크플로우를 사용하여 광고를 `AuditudeResolver` 확인합니다.

* **바꾸기** REPLACE 시간 범위의 경우, 첫 `placementInformations` 번째, 하나 `Mode.DELETE` 및 `Mode.REPLACE`하나가 만들어집니다. 타임라인이 `DeleteContentResolver` 먼저 시간 범위를 삭제한 다음 지정된 광고를 타임라인에 `AuditudeResolver` `replaceDuration` 삽입합니다. 지정하지 `replaceDuration` 않으면 서버에서 삽입할 항목을 결정합니다.

이러한 사용자 지정 시간 범위 작업을 지원하기 위해 TVSDK는 다음을 제공합니다.

* 다양한 컨텐츠 해상도

   스트림에는 광고 신호 모드 및 광고 메타데이터를 기반으로 하는 여러 개의 컨텐츠 해상도가 있을 수 있습니다. 비헤이비어는 다양한 광고 신호 모드 및 광고 메타데이터 조합으로 변경됩니다.
* 다중 초기 `PlacementInformations` 광고 `DefaultMediaPlayer` 신호 모드를 `PlacementInformations` 기반으로 하는 초기 목록과 광고 메타데이터를 `MediaPlayerClient`만듭니다.

* 새로운 광고 신호 모드:사용자 지정 시간 범위

   광고는 외부 소스(JSON 파일 등)의 시간 범위 데이터를 기반으로 배치됩니다.