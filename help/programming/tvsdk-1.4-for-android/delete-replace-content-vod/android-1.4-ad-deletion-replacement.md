---
description: Android TVSDK API에서 이러한 변경 사항은 광고 삭제 및 대체를 지원합니다.
seo-description: Android TVSDK API에서 이러한 변경 사항은 광고 삭제 및 대체를 지원합니다.
seo-title: 광고 삭제 및 교체 API 변경 사항
title: 광고 삭제 및 교체 API 변경 사항
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 광고 삭제 및 교체 API 변경 사항{#ad-deletion-and-replacement-api-changes}

Android TVSDK API에서 이러한 변경 사항은 광고 삭제 및 대체를 지원합니다.

* `AdSignalingMode` 새로운 사용자 지정 시간 범위 광고 신호 모드

* `AdvertisingMetadata` 새로운 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`기능:메타데이터를 처리할 때 표시, 삭제 또는 대체할 시간 범위를 설정합니다.

* `ContentResolver`

   * 새로운 기능 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 새로운 기능 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 새 `ContentRemoval` 클래스

   `TimelineOperation` 타임라인에서 제거할 시간 범위를 정의하는 클래스입니다.

* `AuditudeResolver`

   * 새로운 기능 `private LinkedList<AuditudeRequest> _requestQueue`
   * 새로운 `void startConsumer()`기능:Primetime 광고 결정 요청 큐 처리를 시작하고 `MIN_INIT_REQUEST_INTERVAL` 간격으로 각 요청이 발행되었는지 확인합니다

   * 새로운 `processReplacementRange()`기능:광고 메타데이터에서 시간 범위를 추출하고 `PlacementInformations`이를 포함하는 Primetime 광고 결정 요청을 생성합니다 `PlacementInformations`.

   * 새로운 `canDoResolver()`기능:배치 기회에 Primetime 광고 결정 메타데이터가 있는지 확인

* 광고 `CustomRangeHelper` 메타데이터에서 시간 범위 메타데이터를 추출하고 하위 세트/겹침/잘못된 시간 범위를 제거하는 새로운 도우미 클래스입니다.

* 새 `DeleteContentResolver` 컨텐츠 확인자는 `PlacementInformation.Mode.DELETE`

* 새로운 `NopTimelineOperation` 새로운 타임라인 연산을 통해 광고 중단 배치 또는 교체가 필요 없는 경우 수행할 수 있습니다. 이 클래스는 해결 프로세스 중에 오류가 발생하는 경우와 이를 구분하는 데 사용됩니다.

* `TimelineOperationQueue` [타임라인 작업]이 처리 `NopTimelineOperation` 전인지 확인합니다.

* `CustomAdMarkersContentResolver` 새로운 `canDoResolve()`기능:배치 기회가 유형인지 확인 `Mode.MARK`

* `MetadataResolver` 새로운 `canDoResolve()`기능:배치 기회가 유형인지 확인 `Mode.INSERT`

* `DefaultMetadataKeys` 새로운 기능 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 새 모드 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 새 유형 `CUSTOM_TIME_RANGES`

* `TimeRange` 새로운 `compareTo(TimeRange timeRange)`기능:따라서 시작 시간을 기준으로 TimeRange를 정렬할 수 있습니다.

* 새로운 `ReplacementTimeRange` 기능 대체 시간 범위를 나타내는 `TimeRange` 클래스를 `begin`매개 변수, `end`및 `replacement-duration` 매개 변수로 확장합니다.

* `TimeRangeCollection`

   * 새로운 기능 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 다음으로 `CUSTOM_AD_MARKERS` 이름 변경 `MARK_RANGES`

   * 삭제/표시/바꾸기 범위를 광고 메타데이터에 `toMetadata(Metadata options)` 넣도록 수정되었습니다.

* `MediaPlayerNotification`

   * 새로운 `UNDEFINED_TIME_RANGES`기능:광고 신호 모드가 서버 맵 또는 매니페스트 큐이고 대체 범위가 광고 메타데이터에도 있으면 대체 범위가 무시됩니다.
   * 새로운 `REPLACE_RANGES_NOT_AVAILABLE`기능:광고 신호 모드가 사용자 지정 시간 범위이고 대체 범위를 사용할 수 없는 경우 경고가 전달됩니다.

* `AdvertisingFactory` 새로운 기능 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 새로운 기능 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 새로운 기능 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 위치 `prepareToPlay()`:범위가 `[0,n]` 삭제되면 미디어 플레이어가 자동으로 재생되지 않으므로 초기 검색을 0으로 만듭니다.

   * 위치 `prepareToPlay()`:해결할 초기 배치 정보 목록을 `mediaplayerclient` 반복합니다.

   * 위치 `extractAdSignalingMode()`:새로운 사용자 지정 시간 범위 모드를 수용합니다.
   * 새로운 `private static List<PlacementInformation> createInitalPlacementInformations()`기능:광고 신호 모드 및 컨텐츠 해상도(광고 메타데이터에서 파생된)에 대한 초기 배치 정보를 생성합니다.
   * 위치 `ContentPlacementCompletedListener`:전화하기 `mediaPlayerClient` 전에 있는지 여부를 `doneInitialResolving` 확인합니다 `endAdResolving`.

* `MediaPlayerClient`

   * 새로운 기능 `List<ContentResolver> _contentResolvers`
   * 새로운 기능 `int _reservations`
   * 새로운 `lookupContentResolver(PlacementOpportunity placementOpportunity)`기능:문제를 해결할 수 있는 해결 프로그램을 `PlacementOpportunity`찾습니다.

   * 여러 컨텐츠 해상도 제작을 위해 코드를 수정했습니다.
   * 새로운 `public boolean doneInitialResolving()`기능:해결해야 할 기회가 남아 있는지 확인합니다.

* `VideoEngineTimeline`

   * 새로운 `removeContent(TimelineOperation timelineOperation)`기능:타임라인에서 지정된 컨텐츠 범위를 제거합니다.
   * 새로운 `removeContentByLocalTime(long begin, long end)`기능:지정된 `begin` 시간과 `end`지정된 시간별로 컨텐츠를 제거합니다.

* `DefaultOpportunityDetectorFactory` 수정됨 `createOpportunityDetector`:VOD 스트림의 경우, MARK 또는 REPLACE 범위가 없는 `SpliceOutOpportunityDetector` 경우에만 새로 반환합니다(이러한 범위의 우선 순위는 신호 모드보다 우선함).

