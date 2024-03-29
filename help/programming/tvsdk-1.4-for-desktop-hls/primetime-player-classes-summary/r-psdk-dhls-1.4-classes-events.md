---
description: 이러한 클래스는 TVSDK가 다양한 활동에 대한 응답으로 미디어 플레이어에 전달하는 이벤트를 설명합니다.
title: Events 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Events 클래스 {#events-classes}

이러한 클래스는 TVSDK가 다양한 활동에 대한 응답으로 미디어 플레이어에 전달하는 이벤트를 설명합니다.

패키지: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 이름 | 의미 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 클래스. 광고 브레이크가 시작되거나 완료되었습니다. |
| [AdClickevent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 클래스. 사용자가 광고를 클릭했습니다. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 클래스. 플레이어가 광고를 재생했습니다. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 클래스. 플레이어가 버퍼링을 시작하거나 중지했습니다. |
| [사용자 지정 광고 이벤트](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-1-4-for-desktop-hls/advertising/custom-ads/r-psdk-dhls-1.4-custom-ad-events.html?lang=en) | 클래스. 플레이어는 사용자 지정 광고 로드 상태를 표시하며 오류가 있거나 로드하는 데 너무 오래 걸리는 광고를 무시할 수 있습니다. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 클래스. 새 DRM 메타데이터가 현재 항목과 연결됩니다. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 클래스. 재생 중인 현재 미디어 스트림에 대한 다운로드 정보를 사용할 수 있습니다. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 클래스. 미디어 플레이어 항목이 생성되었습니다. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 클래스. 로드 작업이 완료되었습니다. 발송자: `MediaPlayerItemLoader` 클라이언트에 알립니다. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 클래스. 미디어 플레이어 상태가 변경되었습니다. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 클래스. 다음 `MediaPlayerView` 을(를) 클릭했습니다. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 클래스. 미디어 플레이어의 재생 속도가 변경됩니다. |
| [프로필 이벤트](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 클래스. 미디어 플레이어의 적응 비트 레이트 스위칭 알고리즘은 네트워크 또는 기계 조건에 의해 다른 프로파일로 전환되었다. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 클래스. 플레이어가 찾기를 시작했거나 찾기 작업이 완료되었습니다. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 클래스. 비디오 크기를 사용할 수 있습니다. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 클래스. 미디어 플레이어의 상태가 변경되었습니다. |
| [TimedMetaEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 클래스. 시간 초과된 메타데이터는 기회 감지기에 의해 처리됩니다. |
| [타임라인 이벤트](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 클래스. 미디어 플레이어 타임라인이 변경되었습니다. |
