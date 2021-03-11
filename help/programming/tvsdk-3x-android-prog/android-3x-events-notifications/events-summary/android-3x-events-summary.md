---
description: 응용 프로그램은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변화하는 상태를 모니터링할 수 있습니다.
title: Primetime 플레이어 이벤트 요약
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Primetime 플레이어 이벤트 요약 {#primetime-player-events-summary}

응용 프로그램은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변화하는 상태를 모니터링할 수 있습니다.

## 이벤트 {#events}

응용 프로그램이 응답해야 하는 이벤트가 발생하면 TVSDK에서 사용자에게 알립니다. 각 이벤트는 구현해야 하는 콜백 메서드와 함께 리스너 클래스에 해당합니다.

>[!TIP]
>
>이벤트 코드는 `MediaPlayerEvent` 열거형의 상수입니다.

`AdBreakCompletedEventListener`

* **의미** 광고 브레이크의 재생이 완료되었습니다.

* **구현할 콜백** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **이벤트 코드** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** 의미 재생 중에 광고 나누기를 건너뛰었습니다.

* **구현할 콜백** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **이벤트 코드** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **의미** 광고 중단의 재생이 시작되었습니다.

* **구현할 콜백** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **이벤트 코드** `AD_BREAK_START`

`AdClickedEventListener`

* **** 의미 재생 중에 광고를 클릭했습니다.

* **구현할 콜백** `onAdClicked(AdClickEvent event)`
* **이벤트 코드** `AD_CLICK`

`AdCompletedEventListener`

* **** 의미 광고 재생이 완료되었음을 나타냅니다.

* **구현할 콜백** `onAdCompleted(AdPlaybackEvent event)`

* **이벤트 코드** `AD_COMPLETE`

`AdProgressEventListener`

* **의미** 재생 중 진행 상황을 보고합니다.

* **구현할 콜백** `onAdProgress(AdPlaybackEvent event)`

* **이벤트 코드** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** 의미: Primetime 광고 결정 광고 해상도가 완료되었습니다. 이 이벤트는 VOD 컨텐츠에만 해당됩니다.

* **구현할 콜백** `onAdResolutionComplete()`

* **이벤트 코드** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** 의미 광고 재생이 시작되었습니다.

* **구현할 콜백** `onAdStarted(AdPlaybackEvent event)`

* **이벤트 코드** `AD_START`

`AudioUpdatedEventListener`

* **의미** 새 오디오 트랙이 검색되었습니다.

* **구현할 콜백** `onAudioUpdated(MediaPlayerItemEvent event)`

* **이벤트 코드** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** 의미 플레이어가 버퍼링을 시작했습니다.

* **구현할 콜백** `onBufferingBegin(BufferEvent event)`

* **이벤트 코드** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** 의미 플레이어가 버퍼링을 중지했습니다.

* **구현할 콜백** `onBufferingEnd(BufferEvent event)`

* **이벤트 코드** `BUFFERING_END`

&#39;BufferPreparedEventListener&quot;

* **** 의미 버퍼가 준비되었습니다.

* **구현할 콜백** `onBufferPrepared()`

* **이벤트 코드** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **의미** 새 캡션 트랙이 검색되었습니다.

* **구현할 콜백** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **이벤트 코드** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** 의미 미디어 스트림에서 새 DRM 메타데이터가 검색되었습니다.

* **구현할 콜백** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **이벤트 코드** `DRM_METADATA`

`ItemCreatedEventListener`

* **** 의미 새 미디어 플레이어 항목이 만들어졌습니다.

* **구현할 콜백** `onItemCreated(MediaPlayerItemEvent event)`

* **이벤트 코드** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** 의미 현재 항목에 대해 새 로드 정보가 만들어졌습니다.

* **구현할 콜백** `onLoadComplete(MediaPlayerItemEvent event)`

* **이벤트 코드** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** 의미 새 세그먼트가 로드되었습니다.

* **구현할 콜백** `onLoadInformation(LoadInformationEvent event)`

* **이벤트 코드** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **의미** 주 매니페스트 또는 재생 목록이 업데이트되었습니다.

* **구현할 콜백** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **이벤트 코드** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** 의미 작업이 실패했습니다.

* **구현할 콜백** `onNotification(NotificationEvent event)`

* **이벤트 코드** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** 의미 재생 범위가 업데이트되었습니다.

* **구현할 콜백** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **이벤트 코드** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** 의미 새로운 재생 속도가 화면에 표시됩니다.

* **구현할 콜백** `onRatePlaying(PlaybackRateEvent event)`

* **이벤트 코드** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** 의미 MediaPlayer의 rate 속성이 설정되었습니다.

* **구현할 콜백** `onRateSelected(PlaybackRateEvent event)`

* **이벤트 코드** `RATE_SELECTED`

`PlayStartEventListener`

* **** 의미 재생이 시작되었습니다.

* **구현할 콜백** `onPlayStart()`

* **이벤트 코드** `PLAY_START`

`ProfileChangeEventListener`

* **** 의미 MediaPlayer의 현재 프로필이 변경되었습니다.

* **구현할 콜백** `onProfileChanged(ProfileEvent event)`

* **이벤트 코드** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **재생** 이 타임라인 예약에 도달했습니다.

* **구현할 콜백** `onReservationReached(ReservationEvent event)`

* **이벤트 코드** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **의미** Seek 작업이 시작되었습니다.

* **구현할 콜백** `onSeekBegin(SeekEvent event)`

* **이벤트 코드** `SEEK_BEGIN`

`SeekEndEventListener`

* **** 의미 검색 작업이 완료되었습니다.

* **구현할 콜백** `onSeekEnd(SeekEvent event)`

* **이벤트 코드** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **의미** 내부 재생 규칙 또는 외부 비즈니스 규칙으로 검색 위치가 조정되었습니다.

* **구현할 콜백** `onPositionAdjusted(SeekEvent event)`

* **이벤트 코드** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** 의미 미디어 크기를 사용할 수 있습니다.

* **구현할 콜백** `onSizeAvailable(SizeAvailableEvent event)`

* **이벤트 코드** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** 의미 MediaPlayer 상태가 변경되었습니다.

* **구현할 콜백** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **이벤트 코드** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** 의미재생 헤드가 변경되었습니다.

* **구현할 콜백** `onTimeChanged(TimeChangeEvent event)`

* **이벤트 코드** `TIME_CHANGED`

`TimedEventEventListener`

* **** 의미 작업에 소요되는 시간과 함께 작업이 완료됩니다.

* **구현할 콜백** `onTimedEvent(TimedEventEvent event)`

* **이벤트 코드** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **의미** 새로운 시간 메타데이터가 백그라운드에서 항목에 추가되었습니다.

* **구현할 콜백** `onTimedMetadata(TimedMetadataEvent event)`

* **이벤트 코드** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** 의미 미디어 스트림에서 새 시간 메타데이터가 검색되었습니다.

* **구현할 콜백** `onTimedMetadata(TimedMetadataEvent event)`

* **이벤트 코드** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** 의미 타임라인이 수정되었습니다. 광고가 타임라인에 추가되었거나 타임라인에서 제거되었을 수 있습니다.

* **구현할 콜백** `onTimelineUpdated(TimelineEvent event)`

* **이벤트 코드** `TIMELINE_UPDATED`