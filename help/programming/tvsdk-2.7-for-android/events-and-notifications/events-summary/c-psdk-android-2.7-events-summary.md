---
description: 응용 프로그램은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변화하는 상태를 모니터링할 수 있습니다.
title: Primetime 플레이어 이벤트 요약
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Primetime 플레이어 이벤트 요약 {#primetime-player-events-summary-overview}

응용 프로그램은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변화하는 상태를 모니터링할 수 있습니다.

## 이벤트 {#events}

응용 프로그램이 응답해야 하는 이벤트가 발생하면 TVSDK에서 사용자에게 알립니다. 각 이벤트는 구현해야 하는 콜백 메서드와 함께 리스너 클래스에 해당합니다.

>[!TIP]
>
>이벤트 코드는 `MediaPlayerEvent` 열거형의 상수입니다.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** 의미 ** 광고 브레이크의 재생이 완료되었음을 의미합니다.

* ** 콜백** `onAdBreakCompleted(AdBreakPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_BREAK_COMPLETE`

## AdBreakSwitchedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** 의미 ** 재생 중에 광고 나누기를 건너뛰었습니다.

* ** 콜백** `onAdBreakSkipped(AdBreakPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** 의미 ** 광고 중단 재생이 시작되었습니다.

* ** 콜백** `onAdBreakStarted(AdBreakPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** 의미 ** 재생 중에 광고를 클릭했습니다.

* ** 콜백** `onAdClicked(AdClickEvent event)` 구현

* ** 이벤트 코드 ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** 의미 ** 광고 재생이 완료되었음을 의미합니다.

* ** 콜백** `onAdCompleted(AdPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** 재생 도중 진행 상태** 의미하며

* ** 콜백** `onAdProgress(AdPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Primetime 광고 결정** 광고 해상도가 완성되었음을 의미합니다. 이 이벤트는 VOD 컨텐츠에만 해당됩니다.

* ** 콜백** `onAdResolutionComplete()` 구현

* ** 이벤트 코드 ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** 의미 ** 광고 재생이 시작되었습니다.

* ** 콜백** `onAdStarted(AdPlaybackEvent event)` 구현

* ** 이벤트 코드 ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** 의미 ** 새 오디오 트랙이 검색되었습니다.

* ** 콜백** `onAudioUpdated(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** 의미 ** 플레이어가 버퍼링을 시작했습니다.

* ** 콜백** `onBufferingBegin(BufferEvent event)` 구현

* ** 이벤트 코드 ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** 의미 ** 플레이어가 버퍼링을 중지했습니다.

* ** 콜백** `onBufferingEnd(BufferEvent event)` 구현

* ** 이벤트 코드 ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** 의미 ** 버퍼가 준비되었습니다.

* ** 콜백** `onBufferPrepared()` 구현

* ** 이벤트 코드 ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** 의미 ** 새 캡션 트랙이 검색되었습니다.

* ** 콜백** `onCaptionsUpdated(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** 의미 ** 미디어 스트림에서 새 DRM 메타데이터가 검색되었습니다.

* ** 콜백** `onDRMMetadataInfo(DRMMetadataInfoEvent event)` 구현

* ** 이벤트 코드 ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** 의미 ** 새 미디어 플레이어 항목이 만들어졌습니다.

* ** 콜백** `onItemCreated(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** 의미 ** 현재 항목에 대해 새 로드 정보가 생성되었습니다.

* ** 콜백** `onLoadComplete(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** 의미 ** 새 세그먼트가 로드되었습니다.

* ** 콜백** `onLoadInformation(LoadInformationEvent event)` 구현

* ** 이벤트 코드 ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** 의미 ** 기본 매니페스트 또는 재생 목록이 업데이트되었습니다.

* ** 콜백** `onMainManifestUpdated(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** 의미 ** 작업이 실패했습니다.

* ** 콜백** `onNotification(NotificationEvent event)` 구현

* ** 이벤트 코드 ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** 의미 ** 재생 범위가 업데이트되었습니다.

* ** 콜백** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)` 구현

* ** 이벤트 코드 ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** 의미 ** 새로운 재생 속도가 화면에 표시됩니다.

* ** 콜백** `onRatePlaying(PlaybackRateEvent event)` 구현

* ** 이벤트 코드 ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** 의미 ** MediaPlayer의 rate 속성이 설정되었습니다.

* ** 콜백** `onRateSelected(PlaybackRateEvent event)` 구현

* ** 이벤트 코드 ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **** 재생이 시작되었습니다.

* ** 콜백** `onPlayStart()` 구현

* ** 이벤트 코드 ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** 의미 ** MediaPlayer의 현재 프로필이 변경되었습니다.

* ** 콜백** `onProfileChanged(ProfileEvent event)` 구현

* ** 이벤트 코드 ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** 재생** 타임라인 예약에 도달했습니다.

* ** 콜백** `onReservationReached(ReservationEvent event)` 구현

* ** 이벤트 코드 ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** 검색 작업** 시작되었음을 의미합니다.

* ** 콜백** `onSeekBegin(SeekEvent event)` 구현

* ** 이벤트 코드 ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** 의미 ** 검색 작업이 완료되었습니다.

* ** 콜백** `onSeekEnd(SeekEvent event)` 구현

* ** 이벤트 코드 ** `SEEK_END`

## SeekPositionAdjutedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** 의미 ** 내부 재생 규칙 또는 외부 비즈니스 규칙으로 검색 위치가 조정되었습니다.

* ** 콜백** `onPositionAdjusted(SeekEvent event)` 구현

* ** 이벤트 코드 ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** 의미 ** 미디어 크기를 사용할 수 있습니다.

* ** 콜백** `onSizeAvailable(SizeAvailableEvent event)` 구현

* ** 이벤트 코드 ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **** MediaPlayer 상태가 변경되었습니다.

* ** 콜백** `onStatusChanged(MediaPlayerStatusChangeEvent event)` 구현

* ** 이벤트 코드 ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **** 재생 헤드가 변경되었습니다.

* ** 콜백** `onTimeChanged(TimeChangeEvent event)` 구현

* ** 이벤트 코드 ** `TIME_CHANGED`

## TimedEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** 의미 ** 작업에 소요되는 시간과 함께 작업이 완료됩니다.

* ** 콜백** `onTimedEvent(TimedEventEvent event)` 구현

* ** 이벤트 코드 ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** 의미 ** 새로운 시간 지정 메타데이터가 백그라운드에서 항목에 추가되었습니다.

* ** 콜백** `onTimedMetadata(TimedMetadataEvent event)` 구현

* ** 이벤트 코드 ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** 의미 ** 미디어 스트림에서 새 시간 메타데이터가 검색되었습니다.

* ** 콜백** `onTimedMetadata(TimedMetadataEvent event)` 구현

* ** 이벤트 코드 ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** 의미 ** 타임라인이 수정되었습니다. 광고가 타임라인에 추가되었거나 타임라인에서 제거되었을 수 있습니다.

* ** 콜백** `onTimelineUpdated(TimelineEvent event)` 구현

* ** 이벤트 코드 ** `TIMELINE_UPDATED`