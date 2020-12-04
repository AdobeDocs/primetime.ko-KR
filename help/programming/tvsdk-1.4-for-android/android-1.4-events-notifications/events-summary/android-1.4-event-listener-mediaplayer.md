---
description: TVSDK는 광고 재생이 시작되는 시기 등 광고 관련 작업에 대한 응답으로 광고 재생 이벤트를 전달합니다.
seo-description: TVSDK는 광고 재생이 시작되는 시기 등 광고 관련 작업에 대한 응답으로 광고 재생 이벤트를 전달합니다.
seo-title: 광고 재생 이벤트
title: 광고 재생 이벤트
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# 광고 재생 이벤트{#ad-playback-events}

TVSDK는 광고 재생이 시작되는 시기 등 광고 관련 작업에 대한 응답으로 광고 재생 이벤트를 전달합니다.

모든 광고 재생 관련 이벤트에 대한 알림을 받으려면 다음 콜백을 포함한 `MediaPlayer.AdPlaybackEventListener` 구현을 등록하십시오.

>[!TIP]
>
>광고가 미디어에 삽입되거나 미디어에서 제거되면 TVSDK는 재생 이벤트 [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated())을 전달합니다.

| 이벤트 | 의미 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 광고 중단이 완전히 이루어졌다. |
| onAdBreakBrigled | 재생하는 동안 광고 나누기를 건너뛰었습니다. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 광고 중단이 시작되었습니다. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, 광고, AdClick adClick) | 사용자가 광고를 클릭했습니다. 애플리케이션이 `MediaPlayerView`에서 `notifyClick`을(를) 호출하는 동안 사용자가 클릭한 광고에 대한 정보를 애플리케이션에 제공합니다. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, 광고) | 광고가 완전히 나왔다. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, 광고, int 백분율) | 광고 재생 속도가 빨라졌습니다. 광고가 재생되는 동안 여러 번 전달됩니다. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, 광고) | 광고가 시작되었습니다. |