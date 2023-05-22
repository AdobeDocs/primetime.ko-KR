---
description: 애플리케이션은 TVSDK에서 발송하는 이벤트를 수신하여 플레이어의 활동 및 플레이어의 변화하는 상태를 모니터링할 수 있습니다.
title: Primetime 플레이어 이벤트 요약
exl-id: 42489abe-ccaf-4b40-bb4b-de8547b5585a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Primetime 플레이어 이벤트 요약 {#primetime-player-events-summary-overview}

애플리케이션은 TVSDK에서 발송하는 이벤트를 수신하여 플레이어의 활동 및 플레이어의 변화하는 상태를 모니터링할 수 있습니다.

## 이벤트 {#events}

TVSDK는 애플리케이션이 응답해야 하는 이벤트가 발생하면 알려줍니다. 각 이벤트는 구현해야 하는 콜백 메서드를 사용하는 리스너 클래스에 해당합니다.

>[!TIP]
>
>이벤트 코드는 `MediaPlayerEvent` 열거형.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** 의미 ** 광고 브레이크 재생이 완료되었습니다.

* **을 구현하는 콜백 ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_BREAK_COMPLETE`

## AdBreakSkipEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** 의미 ** 재생 중에 광고 브레이크를 건너뛰었습니다.

* **을 구현하는 콜백 ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** 의미 ** 광고 브레이크 재생이 시작되었습니다.

* **을 구현하는 콜백 ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** 의미 ** 재생 중에 클릭한 광고입니다.

* **을 구현하는 콜백 ** `onAdClicked(AdClickEvent event)`

* ** 이벤트 코드 ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** 의미 ** 광고 재생이 완료되었습니다.

* **을 구현하는 콜백 ** `onAdCompleted(AdPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** 재생 중** 보고 진행률을 의미합니다.

* **을 구현하는 콜백 ** `onAdProgress(AdPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Primetime ** decisioning 광고 해결이 완료되었음을 의미합니다. 이 이벤트는 VOD 콘텐츠에만 적용할 수 있습니다.

* **을 구현하는 콜백 ** `onAdResolutionComplete()`

* ** 이벤트 코드 ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** 의미 ** 광고 재생이 시작되었습니다.

* **을 구현하는 콜백 ** `onAdStarted(AdPlaybackEvent event)`

* ** 이벤트 코드 ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** 의미 ** 새 오디오 트랙이 감지되었습니다.

* **을 구현하는 콜백 ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** 플레이어** 버퍼링을 시작했습니다.

* **을 구현하는 콜백 ** `onBufferingBegin(BufferEvent event)`

* ** 이벤트 코드 ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** 플레이어** 버퍼링을 중지했음을 의미합니다.

* **을 구현하는 콜백 ** `onBufferingEnd(BufferEvent event)`

* ** 이벤트 코드 ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** 버퍼** 준비되었다는 의미입니다.

* **을 구현하는 콜백 ** `onBufferPrepared()`

* ** 이벤트 코드 ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** 의미 ** 새 캡션 트랙이 감지되었습니다.

* **을 구현하는 콜백 ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** 의미 ** 미디어 스트림에서 새 DRM 메타데이터가 감지되었습니다.

* **을 구현하는 콜백 ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** 이벤트 코드 ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** 의미 ** 새 미디어 플레이어 항목이 생성되었습니다.

* **을 구현하는 콜백 ** `onItemCreated(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** 의미 ** 현재 항목에 대한 새 로드 정보가 생성되었습니다.

* **을 구현하는 콜백 ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** 의미 ** 새 세그먼트가 로드되었습니다.

* **을 구현하는 콜백 ** `onLoadInformation(LoadInformationEvent event)`

* ** 이벤트 코드 ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdateEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** 의미 ** 기본 매니페스트 또는 재생 목록이 업데이트되었습니다.

* **을 구현하는 콜백 ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `MANIFEST_UPDATED`

## 알림 이벤트 수신기 {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** 작업** 실패했음을 의미합니다.

* **을 구현하는 콜백 ** `onNotification(NotificationEvent event)`

* ** 이벤트 코드 ** `OPERATION_FAILED`

## PlaybackRangeUpdateEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** 의미 ** 재생 범위가 업데이트되었습니다.

* **을 구현하는 콜백 ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** 이벤트 코드 ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** 의미 ** 새 재생 속도가 화면에 표시됩니다.

* **을 구현하는 콜백 ** `onRatePlaying(PlaybackRateEvent event)`

* ** 이벤트 코드 ** `RATE_PLAYING`

## 재생 속도 선택 이벤트 리스너 {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** MediaPlayer** 속도 속성이 설정되었음을 의미합니다.

* **을 구현하는 콜백 ** `onRateSelected(PlaybackRateEvent event)`

* ** 이벤트 코드 ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** 의미 ** 재생이 시작되었습니다.

* **을 구현하는 콜백 ** `onPlayStart()`

* ** 이벤트 코드 ** `PLAY_START`

## ProfileChangeEventListen {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** MediaPlayer** 현재 프로필이 변경되었음을 의미합니다.

* **을 구현하는 콜백 ** `onProfileChanged(ProfileEvent event)`

* ** 이벤트 코드 ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** 재생** 타임라인 예약에 도달했음을 의미합니다.

* **을 구현하는 콜백 ** `onReservationReached(ReservationEvent event)`

* ** 이벤트 코드 ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** 의미 ** 찾기 작업이 시작되었습니다.

* **을 구현하는 콜백 ** `onSeekBegin(SeekEvent event)`

* ** 이벤트 코드 ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** 의미 ** 검색 작업이 완료되었습니다.

* **을 구현하는 콜백 ** `onSeekEnd(SeekEvent event)`

* ** 이벤트 코드 ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** 의미 ** 내부 재생 규칙 또는 외부 비즈니스 규칙으로 인해 찾기 위치가 조정되었습니다.

* **을 구현하는 콜백 ** `onPositionAdjusted(SeekEvent event)`

* ** 이벤트 코드 ** `SEEK_POSITION_ADJUSTED`

## 크기 사용 가능한 이벤트 리스너 {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** 의미 ** 미디어 크기를 사용할 수 있습니다.

* **을 구현하는 콜백 ** `onSizeAvailable(SizeAvailableEvent event)`

* ** 이벤트 코드 ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** MediaPlayer 상태** 변경되었습니다.

* **을 구현하는 콜백 ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** 이벤트 코드 ** `STATUS_CHANGED`

## TimeChangeEventListen {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** 플레이헤드** 변경되었습니다.

* **을 구현하는 콜백 ** `onTimeChanged(TimeChangeEvent event)`

* ** 이벤트 코드 ** `TIME_CHANGED`

## TimedEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** 의미 ** 작업에 소요되는 시간으로 작업이 완료됩니다.

* **을 구현하는 콜백 ** `onTimedEvent(TimedEventEvent event)`

* ** 이벤트 코드 ** `TIMED_EVENT`

## 타임라인 메타데이터추가됨InBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** 의미 ** 새로운 시간 지정 메타데이터가 배경의 항목에 추가되었습니다.

* **을 구현하는 콜백 ** `onTimedMetadata(TimedMetadataEvent event)`

* ** 이벤트 코드 ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** 의미 ** 미디어 스트림에서 새 시간 메타데이터가 감지되었습니다.

* **을 구현하는 콜백 ** `onTimedMetadata(TimedMetadataEvent event)`

* ** 이벤트 코드 ** `TIMED_METADATA_AVAILABLE`

## 타임라인UpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** 타임라인** 수정되었다는 의미입니다. 광고가 타임라인에서 추가되거나 제거되었을 수 있습니다.

* **을 구현하는 콜백 ** `onTimelineUpdated(TimelineEvent event)`

* ** 이벤트 코드 ** `TIMELINE_UPDATED`
