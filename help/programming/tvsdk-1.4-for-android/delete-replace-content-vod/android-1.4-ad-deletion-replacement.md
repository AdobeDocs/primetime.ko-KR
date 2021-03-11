---
description: Android TVSDK API에서 이러한 변경 사항은 광고 삭제 및 바꾸기를 지원합니다.
title: 광고 삭제 및 교체 API 변경 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# 광고 삭제 및 교체 API 변경 사항{#ad-deletion-and-replacement-api-changes}

Android TVSDK API에서 이러한 변경 사항은 광고 삭제 및 바꾸기를 지원합니다.

* `AdSignalingMode` 새로운 사용자 지정 시간 범위 광고 신호 모드

* `AdvertisingMetadata` 새로운 기능  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`:메타데이터를 처리할 때 표시, 삭제 또는 대체할 시간 범위를 설정합니다.

* `ContentResolver`

   * 새 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 새 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 새 `ContentRemoval` 클래스

   `TimelineOperation` 타임라인에서 제거할 시간 범위를 정의하는 클래스입니다.

* `AuditudeResolver`

   * 새 `private LinkedList<AuditudeRequest> _requestQueue`
   * 새 `void startConsumer()`:Primetime 광고 결정 요청 큐 처리를 시작하고 각 요청이 `MIN_INIT_REQUEST_INTERVAL` 간격으로 실행되었는지 확인합니다.

   * 새 `processReplacementRange()`:광고 메타데이터에서 시간 범위를 추출하고 `PlacementInformations`을 생성하고 `PlacementInformations`를 포함하는 Primetime 광고 결정 요청을 만듭니다.

   * 새 `canDoResolver()`:배치 기회에 Primetime 광고 결정 메타데이터가 있는지 확인

* 새 `CustomRangeHelper` 광고 메타데이터에서 시간 범위 메타데이터를 추출하고 하위 세트/겹침/잘못된 시간 범위를 제거하는 도우미 클래스입니다.

* `PlacementInformation.Mode.DELETE`의 배치 기회를 해결하는 새 `DeleteContentResolver` 내용 해결 프로그램

* 새 `NopTimelineOperation` 광고 분리 배치 또는 대체를 수행할 필요가 없을 때 새 타임라인 작업을 수행합니다. 이 클래스는 해결 프로세스 중에 오류가 발생하는 경우와 이를 구분하는 데 사용됩니다.

* `TimelineOperationQueue` [타임라인 작업]이 처리  `NopTimelineOperation` 전 상태인지 확인합니다.

* `CustomAdMarkersContentResolver` 새로운 기능  `canDoResolve()`:배치 기회가 유형인지 확인합니다.  `Mode.MARK`

* `MetadataResolver` 새로운 기능  `canDoResolve()`:배치 기회가 유형인지 확인합니다.  `Mode.INSERT`

* `DefaultMetadataKeys` 새로운 기능  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 새 모드 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 새 유형 `CUSTOM_TIME_RANGES`

* `TimeRange` 새로운 기능  `compareTo(TimeRange timeRange)`:시작 시간을 기준으로 TimeRanges를 정렬할 수 있습니다.

* 새 `ReplacementTimeRange` `begin`, `end` 및 `replacement-duration` 매개 변수를 사용하여 대체 시간 범위를 나타내는 `TimeRange` 클래스를 확장합니다.

* `TimeRangeCollection`

   * 새 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * `CUSTOM_AD_MARKERS`을(를) `MARK_RANGES`(으)로 이름이 변경되었습니다.

   * 삭제/표시/바꾸기 범위를 광고 메타데이터에 추가하기 위해 `toMetadata(Metadata options)`을(를) 수정했습니다.

* `MediaPlayerNotification`

   * 새 `UNDEFINED_TIME_RANGES`:광고 신호 모드가 서버 맵 또는 매니페스트 큐이며 대체 범위도 광고 메타데이터에 있으면 대체 범위가 무시됩니다.
   * 새 `REPLACE_RANGES_NOT_AVAILABLE`:광고 신호 모드가 사용자 지정 시간 범위이고 대체 범위를 사용할 수 없는 경우 경고가 전달됩니다.

* `AdvertisingFactory` 새로운 기능  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 새로운 기능  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 새로운 기능  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * `prepareToPlay()`에서:범위 `[0,n]`이(가) 삭제되면 미디어 플레이어가 자동으로 재생되지 않으므로 0으로 초기 검색을 합니다.

   * `prepareToPlay()`에서:`mediaplayerclient`에서 확인할 초기 배치 정보 목록을 반복합니다.

   * `extractAdSignalingMode()`에서:새로운 사용자 지정 시간 범위 모드를 수용할 수 있습니다.
   * 새 `private static List<PlacementInformation> createInitalPlacementInformations()`:광고 신호 모드 및 컨텐츠 해상도에 대한 초기 배치 정보를 생성합니다(광고 메타데이터에서 파생됨).
   * `ContentPlacementCompletedListener`에서:`endAdResolving`을(를) 호출하기 전에 `mediaPlayerClient`이 `doneInitialResolving`인지 확인합니다.

* `MediaPlayerClient`

   * 새 `List<ContentResolver> _contentResolvers`
   * 새 `int _reservations`
   * 새 `lookupContentResolver(PlacementOpportunity placementOpportunity)`:`PlacementOpportunity`을(를) 확인할 수 있는 해결 프로그램을 찾습니다.

   * 여러 컨텐츠 해상도를 만들기 위해 코드를 수정했습니다.
   * 새 `public boolean doneInitialResolving()`:해결할 기회가 남아 있는지 확인합니다.

* `VideoEngineTimeline`

   * 새 `removeContent(TimelineOperation timelineOperation)`:타임라인에서 지정된 컨텐츠 범위를 제거합니다.
   * 새 `removeContentByLocalTime(long begin, long end)`:지정된 로컬 시간별로 `begin` 및 `end`의 컨텐츠를 제거합니다.

* `DefaultOpportunityDetectorFactory` 수정됨  `createOpportunityDetector`:VOD 스트림의 경우 MARK 또는 REPLACE 범위가 없는  `SpliceOutOpportunityDetector` 경우에만 새로 반환합니다(해당 범위는 신호 모드보다 우선순위가 높음).

