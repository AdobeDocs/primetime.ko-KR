---
description: Android TVSDK API의 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.
title: 광고 삭제 및 대체 API 변경 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# 광고 삭제 및 대체 API 변경 사항{#ad-deletion-and-replacement-api-changes}

Android TVSDK API의 이러한 변경 사항은 광고 삭제 및 교체를 지원합니다.

* `AdSignalingMode` 새로운 사용자 지정 시간 범위 광고 신호 모드

* `AdvertisingMetadata` 신규 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: 메타데이터를 처리할 때 표시, 삭제 또는 대체할 시간 범위를 설정합니다

* `ContentResolver`

   * 신규 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 신규 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 신규 `ContentRemoval` 클래스

  `TimelineOperation` 타임라인에서 제거할 시간 범위를 정의하는 클래스

* `AuditudeResolver`

   * 신규 `private LinkedList<AuditudeRequest> _requestQueue`
   * 신규 `void startConsumer()`: Primetime ad decisioning 요청 대기열 처리를 시작하고 각 요청이에 발급되는지 확인합니다. `MIN_INIT_REQUEST_INTERVAL` 간격

   * 신규 `processReplacementRange()`: 광고 메타데이터에서 시간 범위를 추출하여 생성 `PlacementInformations`및 를 포함하는 Primetime ad decisioning 요청을 `PlacementInformations`.

   * 신규 `canDoResolver()`: 배치 영업 기회에 Primetime ad decisioning 메타데이터가 있는지 확인합니다.

* 신규 `CustomRangeHelper` 광고 메타데이터에서 시간 범위 메타데이터를 추출하고 하위 집합/중복/잘못된 시간 범위를 제거하는 도우미 클래스입니다.

* 신규 `DeleteContentResolver` 의 배치 기회를 해결하는 콘텐츠 해결사 `PlacementInformation.Mode.DELETE`

* 신규 `NopTimelineOperation` 광고 브레이크 배치 또는 교체를 수행할 필요가 없는 경우에 대한 새로운 타임라인 작업입니다. 이 클래스는 해결 중 오류가 발생하는 경우와 이것을 구분하는 데 사용됩니다.

* `TimelineOperationQueue` 타임라인 작업이 `NopTimelineOperation` 처리 전.

* `CustomAdMarkersContentResolver` 신규 `canDoResolve()`: 배치 영업 기회가 유형인지 확인합니다. `Mode.MARK`

* `MetadataResolver` 신규 `canDoResolve()`: 배치 영업 기회가 유형인지 확인합니다. `Mode.INSERT`

* `DefaultMetadataKeys` 신규 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 새 모드 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 새 유형 `CUSTOM_TIME_RANGES`

* `TimeRange` 신규 `compareTo(TimeRange timeRange)`: 시작 시간을 기준으로 TimeRanges를 정렬할 수 있음

* 신규 `ReplacementTimeRange` 를 확장합니다. `TimeRange` 대체 시간대를 나타내는 클래스로, `begin`, `end`, 및 `replacement-duration` 매개 변수.

* `TimeRangeCollection`

   * 신규 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 이름이 변경됨 `CUSTOM_AD_MARKERS` 끝 `MARK_RANGES`

   * 수정됨 `toMetadata(Metadata options)` 광고 메타데이터에 범위 삭제/표시/바꾸기.

* `MediaPlayerNotification`

   * 신규 `UNDEFINED_TIME_RANGES`: 광고 시그널링 모드가 서버 맵 또는 매니페스트 큐이고 바꾸기 범위가 광고 메타데이터에도 있는 경우 바꾸기 범위가 무시됩니다.
   * 신규 `REPLACE_RANGES_NOT_AVAILABLE`: 광고 시그널링 모드가 사용자 지정 시간 범위이고 바꾸기 범위를 사용할 수 없으면 경고가 발송됩니다.

* `AdvertisingFactory` 신규 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 신규 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 신규 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 위치 `prepareToPlay()`: if 범위가 0이므로 초기 찾기를 0으로 만듭니다. `[0,n]` 이(가) 삭제되면 미디어 플레이어가 자동으로 재생되지 않습니다.

   * 위치 `prepareToPlay()`: 의 초기 배치 정보 목록을 반복합니다. `mediaplayerclient` 해결.

   * 위치 `extractAdSignalingMode()`: 새 사용자 지정 시간 범위 모드에 맞게 조정됩니다.
   * 신규 `private static List<PlacementInformation> createInitalPlacementInformations()`: 광고 시그널링 모드 및 콘텐츠 해결자에 대한 초기 배치 정보를 생성합니다(광고 메타데이터에서 파생).
   * 위치 `ContentPlacementCompletedListener`: 다음을 확인합니다. `mediaPlayerClient` 은(는) `doneInitialResolving` 호출 전 `endAdResolving`.

* `MediaPlayerClient`

   * 신규 `List<ContentResolver> _contentResolvers`
   * 신규 `int _reservations`
   * 신규 `lookupContentResolver(PlacementOpportunity placementOpportunity)`: 문제를 해결할 수 있는 해결 방법을 찾습니다. `PlacementOpportunity`.

   * 여러 콘텐츠 해결자를 만들도록 코드를 수정했습니다.
   * 신규 `public boolean doneInitialResolving()`: 해결할 수 있는 기회가 남아 있는지 확인합니다.

* `VideoEngineTimeline`

   * 신규 `removeContent(TimelineOperation timelineOperation)`: 타임라인에서 주어진 콘텐츠 범위를 제거합니다.
   * 신규 `removeContentByLocalTime(long begin, long end)`: 제공된 현지 시간별로 콘텐츠 제거 `begin` 및 `end`.

* `DefaultOpportunityDetectorFactory` 수정됨 `createOpportunityDetector`: VOD 스트림의 경우 새 스트림만 반환합니다. `SpliceOutOpportunityDetector` MARK 또는 REPLACE 범위가 없는 경우(해당 범위가 신호 모드에 우선하므로)
