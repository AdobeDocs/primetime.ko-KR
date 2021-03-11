---
description: 이러한 클래스는 다양한 활동에 대한 응답으로 TVSDK가 미디어 플레이어에 전달하는 이벤트를 설명합니다.
title: Events 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# 이벤트 클래스 {#events-classes}

이러한 클래스는 다양한 활동에 대한 응답으로 TVSDK가 미디어 플레이어에 전달하는 이벤트를 설명합니다.

패키지:[com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 이름 | 의미 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 클래스. 광고 나누기가 시작되거나 완료되었습니다. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 클래스. 사용자가 광고를 클릭했습니다. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 클래스. 그 선수는 광고를 했다. |
| [버퍼 이벤트](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 클래스. 플레이어가 버퍼링을 시작하거나 중지했습니다. |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | 클래스. 플레이어는 사용자 지정 광고 로드 상태를 표시하고 오류가 있거나 로드하는 데 시간이 너무 오래 걸리는 광고를 무시할 수 있습니다. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 클래스. 새 DRM 메타데이터가 현재 항목과 연결되어 있습니다. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 클래스. 현재 재생 중인 미디어 스트림에 다운로드 정보를 사용할 수 있습니다. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 클래스. 미디어 플레이어 항목이 만들어졌습니다. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 클래스. 로드 작업이 완료되었습니다. 클라이언트에게 알리기 위해 `MediaPlayerItemLoader`에 의해 전달됩니다. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 클래스. 미디어 플레이어 상태가 변경되었습니다. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 클래스. `MediaPlayerView`을(를) 클릭했습니다. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 클래스. 미디어 플레이어의 재생 속도가 변경됩니다. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 클래스. 미디어 플레이어의 응용 비트 전송률 전환 알고리즘이 네트워크 또는 컴퓨터 조건 때문에 다른 프로필로 전환되었습니다. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 클래스. 플레이어가 검색을 시작했거나 검색 작업이 완료되었습니다. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 클래스. 비디오 크기를 사용할 수 있습니다. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 클래스. 미디어 플레이어의 상태가 변경되었습니다. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 클래스. 시간 지정 메타데이터는 Opportunity Detector에 의해 처리됩니다. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 클래스. 미디어 플레이어 타임라인이 변경되었습니다. |