---
description: TVSDK의 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.
title: 광고 삭제 및 대체 API 변경 사항
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 광고 삭제 및 대체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK의 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.

* `AdSignalingMode` 추가됨 `CUSTOM_RANGES` 신호 모드.

* `OpportunityGenerator`  `extractAdSignalingMode()` - 설정 `AdSignalingMode.CUSTOM_RANGES` 대체 범위가 메타데이터에 있는 경우.

* `PlacementType` 추가됨 `CUSTOM_RANGE` 유형.

* `PlacementMode`

   * 추가됨 `DELETE` 모드.
   * 추가됨 `MARK` 모드
   * 추가됨 `FreeReplace` mode - 이 모드는 지속시간이 있지만 순수한 삽입입니다.

* `TimeRange` 더 이상 `final` 클래스

* 추가됨 `ReplaceTimeRange()` 방법

   확장 `TimeRange` 을(를) 가지려면 `replacementDuration` 속성. MARK 및 DELETE 사례의 경우 `replacementDuration` 은(는) 0입니다.

* `TimeRangeCollection`

   * 추가됨 `toReplaceMetadata()` 추출 유틸리티 함수 `timeRanges`.

   * 을(를) (으)로 수정함 `DELETE` 및 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 추가됨 `createCustomTimeRangesFrom()` - JSON 파일에서 MARK/DELETE/REPLACE 사용 사례에 대한 메타데이터를 작성합니다.
   * 제거됨 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 추가됨 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 추가됨 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (변경되지 않음)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 추가됨 `CustomRangesOpportunityGenerator` 메타데이터에 사용자 지정 범위가 포함된 경우
   * `doRetrieveResolvers()`

      * 추가 `CustomRangeResolver` DELETE 및 REPLACE 사용자 정의 범위가 메타데이터에 있는 경우
      * 이동됨 `CustomAdMarkerResolver` 앞에 `AuditudeResolver`


* 추가됨 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 비어 있음 - 업데이트 없음, VOD
   * `doProcess()` 새 유형의 새 배치를 만듭니다. `Placement.Delete_Range`

   * 추가됨 `CustomRangeOppotunityGenerator` 의 생성기 목록 맨 위에 `DefaultContentFactory`따라서 광고 삽입 전에 삭제 범위가 처리됩니다.

   * 추가됨 `createCustomRangeOpportunities` 모든 기회를 만들려면

      MARK - 의 각 유효한 표시 범위에 대해 하나의 영업 기회 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.MARK`

      DELETE - 의 유효한 삭제 범위마다 하나의 영업 기회 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.DELETE`

      REPLACE - 유효한 각 바꾸기 범위에 대해 두 개의 영업 기회:

      1. 다음의 삭제 범위 기회 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.DELETE`.

      1. 의 Primetime 광고 의사 결정 광고 기회 `PlacementType.MID_ROLL` 또는 `PlacementType.PRE_ROLL` 및 `PlacementMode.FREEREPLACE`

* 추가됨 `CustomRangeResolver`:

   * `doCanResolve()` 반환 `true` 삭제 범위용입니다.

   * 추가됨 `createDeleteRangeOperation()` 만들려면 `DeleteRange` 배치용

* 추가됨 `CustomRangeHelper`:

   * 표시/삭제/바꾸기를 추출하는 일반 유틸리티 클래스 `timeRanges` 처리.
   * 추가됨 `extractCustomRangesMetadata()`
   * 추가됨 `extractCustomRanges()`
   * 추가됨 `mergeRanges()` - 충돌 및 하위 집합/병합 해결

* `MediaPlayerTimeline`:

   * &quot;>위치 `executeOperation()`: 작업이 다음과 같은 경우 `DeleteRange`, 작업에서 메서드를 제거하는 호출을 추가했습니다.

   * 위치 `executeOperation()`: 작업이 다음과 같은 경우 `NOPTimelineOperation` (비어 있음 `AdBreaks` 서버에서 컴백), 지우기 호출을 추가했습니다.

   * 추가됨 `onDeleteRangeComplete()`
   * 추가됨 `removeRange()`
   * 위치 `adjustPlacement()`, `PlacementMode.FREEREPLACE` 모드, 기간을 0으로 설정합니다. 이 기간은 요청할 때 더 빨리 필요합니다. `AdBreaks`이 시점에서 순수 삽입이 되려면 0이어야 합니다.

* `VideoEngineTimeline` 추가됨 `removeC3Ad()` - 호출 `removeByLocalTime()` 삭제 범위

* `AdSignalingModeGenerator`

   * `doConfigure()` - 생성된 영업 기회가 없는 경우 해결하지 않음
   * `createInitialOpportunity()` - 초기 영업 기회 생성 안 함 `AdSignalingMode.CUSTOM_RANGE`. 다음 `CustomRangeOpportunityGenerator` 이미 다룹니다.

* `DeleteRange`

   * 확장 `TimelineOperation`.
   * 작성자: `CustomRangeResolver` 삭제 및 교체용(교체의 삭제 부분)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - 포장 허용
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 다음 `accepts()` 다른 배치 유형(프리롤, 미드롤, 포스트롤)의 패킹이 가능하도록 방법을 수정하였다

* `AuditudeRequestHelper` 서버가 광고 매개 변수를 재정의할 수 있도록 하는 버그 수정

* `AuditudeResolver` 다음 `canBePacked()` 패킹을 허용하도록 메서드가 변경되었습니다.

* `CustomAdResolver` 다음 `timeRange` 추출 기능이 제거되었습니다. 한 번에 한 명씩 배치해서 `AdBreakPlacement timelineOperation`.
