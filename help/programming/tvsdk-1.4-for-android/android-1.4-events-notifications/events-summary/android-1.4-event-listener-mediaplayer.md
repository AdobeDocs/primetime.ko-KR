---
description: TVSDK는 광고 재생이 시작되는 시기와 같은 광고 관련 작업에 응답하여 광고 재생 이벤트를 전달합니다.
title: 광고 재생 이벤트
exl-id: f35e3c6f-1d58-4498-9e3b-cbd53e573ef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 광고 재생 이벤트{#ad-playback-events}

TVSDK는 광고 재생이 시작되는 시기와 같은 광고 관련 작업에 응답하여 광고 재생 이벤트를 전달합니다.

모든 광고 재생 관련 이벤트에 대한 알림을 받으려면 의 구현을 등록하십시오. `MediaPlayer.AdPlaybackEventListener` 다음 콜백을 포함합니다.

>[!TIP]
>
>광고가 미디어에 삽입되거나 미디어에서 제거되면 TVSDK가 재생 이벤트를 전달합니다 [onTimelineUpdate](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| 이벤트 | 의미 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 광고 브레이크가 완전히 재생되었습니다. |
| onAdBreakSkipped | 재생 도중 광고 브레이크를 건너뛰었습니다. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 광고 브레이크가 시작되었습니다. |
| [onAdclick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, 광고, AdClick adClick) | 사용자가 광고를 클릭했습니다. 애플리케이션 호출에 대한 응답으로 사용자가 클릭한 광고에 대한 정보를 애플리케이션에 제공합니다 `notifyClick` 다음에 있음 `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, 광고) | 광고가 완전히 재생되었습니다. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, 광고, int 백분율) | 광고 재생이 진행되었습니다. 광고가 재생되는 동안 여러 번 발송되었습니다. |
| [온애드스타트](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, 광고) | 광고가 시작되었습니다. |
