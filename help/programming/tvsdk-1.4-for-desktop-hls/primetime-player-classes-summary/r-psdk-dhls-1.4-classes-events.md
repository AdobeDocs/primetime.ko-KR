---
description: 이러한 클래스는 다양한 활동에 대한 응답으로 TVSDK가 미디어 플레이어에 전달하는 이벤트를 설명합니다.
seo-description: 이러한 클래스는 다양한 활동에 대한 응답으로 TVSDK가 미디어 플레이어에 전달하는 이벤트를 설명합니다.
seo-title: 이벤트 클래스
title: 이벤트 클래스
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 이벤트 클래스 {#events-classes}

이러한 클래스는 다양한 활동에 대한 응답으로 TVSDK가 미디어 플레이어에 전달하는 이벤트를 설명합니다.

패키지: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 이름 | 의미 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 수업. 광고 브레이크가 시작되었거나 완료되었습니다. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 수업. 사용자가 광고를 클릭했습니다. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 수업. 그 선수는 광고를 냈다. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 수업. 플레이어가 버퍼링을 시작하거나 중지했습니다. |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | 수업. 플레이어는 사용자 지정 광고 로드 상태를 표시하고 오류가 있거나 로드하는 데 시간이 너무 오래 걸리는 광고를 무시할 수 있습니다. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 수업. 새 DRM 메타데이터가 현재 항목과 연결됩니다. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 수업. 현재 재생 중인 미디어 스트림에 대한 다운로드 정보를 사용할 수 있습니다. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 수업. 미디어 플레이어 항목이 만들어졌습니다. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 수업. 로드 작업이 완료되었습니다. 클라이언트에 알리기 `MediaPlayerItemLoader` 위해 에 의해 전달됩니다. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 수업. 미디어 플레이어 상태가 변경되었습니다. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 수업. 클릭이 `MediaPlayerView` 이루어졌습니다. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 수업. 미디어 플레이어의 재생 속도가 변경됩니다. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 수업. 네트워크 또는 시스템 조건으로 인해 미디어 플레이어의 응용 비트 전송률 전환 알고리즘이 다른 프로필로 전환되었습니다. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 수업. 플레이어가 검색을 시작했거나 검색 작업이 완료되었습니다. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 수업. 비디오 크기를 사용할 수 있습니다. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 수업. 미디어 플레이어의 상태가 변경되었습니다. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 수업. Opportunity Detector에서 시간 메타데이터를 처리합니다. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 수업. 미디어 플레이어 타임라인이 변경되었습니다. |