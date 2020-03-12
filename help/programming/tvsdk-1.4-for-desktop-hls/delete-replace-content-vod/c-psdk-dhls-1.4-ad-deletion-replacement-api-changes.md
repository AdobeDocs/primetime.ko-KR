---
description: TVSDK에서 이러한 변경 사항은 광고 삭제 및 변경을 지원합니다.
seo-description: TVSDK에서 이러한 변경 사항은 광고 삭제 및 변경을 지원합니다.
seo-title: 광고 삭제 및 교체 API 변경 사항
title: 광고 삭제 및 교체 API 변경 사항
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 광고 삭제 및 교체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK에서 이러한 변경 사항은 광고 삭제 및 변경을 지원합니다.

* `AdSignalingMode` 신호 `CUSTOM_RANGES` 모드가 추가되었습니다.

* `OpportunityGenerator`  - `extractAdSignalingMode()` 대체 범위가 메타데이터에 있는 `AdSignalingMode.CUSTOM_RANGES` 경우 설정합니다.

* `PlacementType` 추가된 `CUSTOM_RANGE` 유형입니다.

* `PlacementMode`

   * 추가된 `DELETE` 모드.
   * 추가된 `MARK` 모드
   * 추가된 `FreeReplace` 모드 - 이 모드는 지속 시간이 있지만 완전히 삽입입니다.

* `TimeRange` 더 이상 `final` 수업이 아닙니다

* 추가된 `ReplaceTimeRange()` 메서드

   속성이 `TimeRange` 있도록 `replacementDuration` 확장합니다. MARK 및 DELETE 케이스의 경우 0입니다. `replacementDuration`

* `TimeRangeCollection`

   * 추출할 유틸리티 `toReplaceMetadata()` 함수를 `timeRanges`추가했습니다.

   * 및 에서 작동하도록 `DELETE` 수정됨 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 추가된 `createCustomTimeRangesFrom()` - JSON 파일에서 MARK/DELETE/REPLACE 사용 사례에 대한 메타데이터를 만듭니다.
   * 제거됨 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 추가됨 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 추가됨 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (변경되지 않음)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 메타데이터에 사용자 지정 범위가 포함되어 `CustomRangesOpportunityGenerator` 있을 때 추가됨
   * `doRetrieveResolvers()`

      * DELETE 및 REPLACE 사용자 지정 범위가 메타데이터에 있을 `CustomRangeResolver` 때 추가
      * 앞으로 `CustomAdMarkerResolver` 이동 `AuditudeResolver`


* 추가됨 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 비어 있음 - 업데이트 없음, VOD
   * `doProcess()` 새 유형의 새 배치 만들기 `Placement.Delete_Range`

   * 의 생성기 목록 `CustomRangeOppotunityGenerator` 맨 위에 추가되었으므로 `DefaultContentFactory`광고 삽입 전에 삭제 범위가 처리됩니다.

   * 모든 기회를 창출하기 `createCustomRangeOpportunities` 위해 추가된 기능

      MARK - 각 유효한 마크 범위 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.MARK`

      DELETE - 각 유효한 삭제 범위에 대해 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.DELETE`

      REPLACE - 각 유효한 교체 범위에 대해 두 가지 기회를 제공합니다.

      1. 및 의 삭제 범위 `PlacementType.CUSTOM_RANGE` 기회입니다 `PlacementMode.DELETE`.

      1. Adobe Primetime 광고 결정 `PlacementType.MID_ROLL` `PlacementType.PRE_ROLL` 및 `PlacementMode.FREEREPLACE`

* 추가된 `CustomRangeResolver`항목:

   * `doCanResolve()` 삭제 범위에 `true` 대해 반환합니다.

   * 배치를 위해 `createDeleteRangeOperation()` 만들기 `DeleteRange` 위해 추가됨

* 추가된 `CustomRangeHelper`항목:

   * Mark/Delete/Replace를 추출하고 처리할 수 있는 일반 유틸리티 클래스입니다. `timeRanges`
   * 추가됨 `extractCustomRangesMetadata()`
   * 추가됨 `extractCustomRanges()`
   * 추가된 `mergeRanges()` - 충돌 및 하위 세트/병합 문제 해결

* `MediaPlayerTimeline`:

   * &quot;> `executeOperation()`in, 작업이 `DeleteRange`있는 경우 작업에서 제거 메서드에 대한 호출을 추가했습니다.

   * 에서 `executeOperation()`작업이 `NOPTimelineOperation` (서버에서 다시 `AdBreaks` 돌아오는 비어 있음)인 경우 지우기 호출을 추가했습니다.

   * 추가됨 `onDeleteRangeComplete()`
   * 추가됨 `removeRange()`
   * 모드에서 `adjustPlacement()`지속 `PlacementMode.FREEREPLACE` 시간을 0으로 설정했습니다. 이 지속 시간은 요청할 때 이전에 필요합니다. 이 `AdBreaks`시점에서 순수한 삽입으로 하려면 0이어야 합니다.

* `VideoEngineTimeline` 추가된 `removeC3Ad()` - 삭제 `removeByLocalTime()` 범위에 대한 호출

* `AdSignalingModeGenerator`

   * `doConfigure()` - 기회가 생성되지 않으면 확인하지 않습니다.
   * `createInitialOpportunity()` - 초기 영업 기회를 만들지 마십시오. `AdSignalingMode.CUSTOM_RANGE`. 이것은 이미 `CustomRangeOpportunityGenerator` 커버입니다.

* `DeleteRange`

   * 확장 `TimelineOperation`.
   * 삭제 및 대체를 `CustomRangeResolver` 위해 작성됨(대체의 삭제 부분)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - 포장 허용
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 다른 배치 유형(프리롤, 미드롤, 포스트롤)의 포장이 가능하도록 방법이 `accepts()` 수정되었습니다.

* `AuditudeRequestHelper` 광고 매개 변수에 대한 서버 재지정을 허용하는 버그 수정

* `AuditudeResolver` 포장이 허용되도록 `canBePacked()` 방법이 변경되었습니다.

* `CustomAdResolver` 추출 `timeRange` 기능이 제거되었습니다. 한 번에 한 명씩 배치해 `AdBreakPlacement timelineOperation`보죠.

