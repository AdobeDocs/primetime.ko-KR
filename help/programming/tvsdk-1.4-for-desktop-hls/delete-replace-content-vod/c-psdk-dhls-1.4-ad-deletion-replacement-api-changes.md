---
description: TVSDK에서 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.
title: 광고 삭제 및 교체 API 변경 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 광고 삭제 및 교체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK에서 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.

* `AdSignalingMode` 신호  `CUSTOM_RANGES` 모드가 추가되었습니다.

* `OpportunityGenerator`  `extractAdSignalingMode()` - 대체 범위가 메타데이터에 있는  `AdSignalingMode.CUSTOM_RANGES` 경우 설정합니다.

* `PlacementType` 추가된  `CUSTOM_RANGE` 유형입니다.

* `PlacementMode`

   * `DELETE` 모드를 추가했습니다.
   * `MARK` 모드를 추가했습니다.
   * 추가된 `FreeReplace` 모드 - 이 모드에는 지속 시간이 있지만 순수한 삽입입니다.

* `TimeRange` 더 이상 클래스가  `final` 아님

* `ReplaceTimeRange()` 메서드를 추가했습니다.

   `TimeRange`을(를) 확장하여 `replacementDuration` 속성을 가집니다. MARK 및 DELETE 케이스의 경우 `replacementDuration`은 0입니다.

* `TimeRangeCollection`

   * `timeRanges` 추출에 `toReplaceMetadata()` 유틸리티 함수를 추가했습니다.

   * `DELETE` 및 `REPLACE`에서 작동하도록 수정됨

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * `createCustomTimeRangesFrom()` 추가 - JSON 파일에서 MARK/DELETE/REPLACE 사용 사례에 대한 메타데이터를 만듭니다.
   * `createCustomAdMarkersMetadataFrom()` 제거됨

* `DefaultMetadataKeys`

   * `CUSTOM_DELETE_RANGES_METADATA_KEY` 추가됨
   * `CUSTOM_REPLACE_RANGES_METADATA_KEY` 추가됨
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (변경되지 않음)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 메타데이터에 사용자 지정 범위가 포함된 경우 에 대해 `CustomRangesOpportunityGenerator`이(가) 추가되었습니다.
   * `doRetrieveResolvers()`

      * 메타데이터에 DELETE 및 REPLACE 사용자 지정 범위가 있는 경우 `CustomRangeResolver` 추가
      * `AuditudeResolver` 앞에 `CustomAdMarkerResolver`을(를) 이동했습니다.


* `CustomRangeOpportunityGenerator` 추가됨

   * `doUpdate()` 비어 있음 - 업데이트 없음, VOD
   * `doProcess()` 새 유형의 새 배치를 만듭니다.  `Placement.Delete_Range`

   * `DefaultContentFactory`의 생성기 목록 맨 위에 `CustomRangeOppotunityGenerator`이 추가되었으므로 광고 삽입 전에 삭제 범위가 처리됩니다.

   * 모든 기회를 만들기 위해 `createCustomRangeOpportunities`을(를) 추가했습니다.

      MARK - 각 유효한 표시 범위의 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.MARK`에 대한 하나의 기회

      DELETE - 각 유효한 삭제 범위 `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.DELETE`에 대해 하나의 기회

      REPLACE - 각 유효한 교체 범위에 대한 두 가지 기회:

      1. `PlacementType.CUSTOM_RANGE` 및 `PlacementMode.DELETE`의 삭제 범위 기회입니다.

      1. `PlacementType.MID_ROLL` 또는 `PlacementType.PRE_ROLL` 및 `PlacementMode.FREEREPLACE`의 Primetime 광고 결정 및 기회

* 추가된 `CustomRangeResolver`:

   * `doCanResolve()` 삭제 범위 `true` 에 대해 반환합니다.

   * 배치를 위해 `DeleteRange`을(를) 만들기 위해 `createDeleteRangeOperation()`을(를) 추가했습니다.

* 추가된 `CustomRangeHelper`:

   * Mark/Delete/Replace `timeRanges`을 추출하고 처리하는 일반 유틸리티 클래스입니다.
   * `extractCustomRangesMetadata()` 추가됨
   * `extractCustomRanges()` 추가됨
   * `mergeRanges()` 추가됨 - 충돌 및 하위 세트/병합 해결

* `MediaPlayerTimeline`:

   * &quot;>작업 `executeOperation()`이(가) `DeleteRange`인 경우 작업에서 제거 메서드 호출을 추가했습니다.

   * `executeOperation()`에서 작업이 `NOPTimelineOperation`(서버에서 다시 돌아오는 빈 `AdBreaks`)인 경우 지우기 호출을 추가했습니다.

   * `onDeleteRangeComplete()` 추가됨
   * `removeRange()` 추가됨
   * `adjustPlacement()`에서 `PlacementMode.FREEREPLACE` 모드의 경우 지속 시간을 0으로 설정했습니다. 이 기간은 `AdBreaks`을(를) 요청할 때 더 일찍 필요합니다. 이 시점에서는 완전 삽입이 되려면 0이어야 합니다.

* `VideoEngineTimeline` 추가된  `removeC3Ad()` - 삭제 범위 `removeByLocalTime()` 에 대한 호출

* `AdSignalingModeGenerator`

   * `doConfigure()` - 기회가 생성되지 않으면 확인하지 않습니다.
   * `createInitialOpportunity()` - 의 초기 기회를 생성하지 마십시오 `AdSignalingMode.CUSTOM_RANGE`. `CustomRangeOpportunityGenerator`이(가) 이미 이것을 포함합니다.

* `DeleteRange`

   * `TimelineOperation`을(를) 확장합니다.
   * 삭제 및 대체를 위해 `CustomRangeResolver`에 의해 생성됨(교체 삭제 부분)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - 포장 허용
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 다른 배치 유형(프리롤, 미드롤, 포스트롤)의 포장이 가능하도록  `accepts()` 방법이 수정되었습니다.

* `AuditudeRequestHelper` 서버 오버라이드가 광고 매개 변수에 적용되도록 하는 버그 수정

* `AuditudeResolver` 포장이  `canBePacked()` 가능하도록 방법이 변경되었습니다

* `CustomAdResolver` 추출  `timeRange` 기능이 제거되었습니다. 한 번에 한 배치만 받고 이를 `AdBreakPlacement timelineOperation`으로 전환합니다.

