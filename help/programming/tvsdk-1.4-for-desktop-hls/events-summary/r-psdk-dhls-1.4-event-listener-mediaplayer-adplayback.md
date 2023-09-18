---
description: TVSDK는 광고 재생이 시작되는 시기와 같은 광고 관련 작업에 응답하여 광고 재생 이벤트를 전달합니다.
title: 광고 재생 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 광고 재생 이벤트 {#ad-playback-events}

TVSDK는 광고 재생이 시작되는 시기와 같은 광고 관련 작업에 응답하여 광고 재생 이벤트를 전달합니다.

모든 광고 재생 관련 이벤트에 대한 알림을 받으려면 수신자를 `MediaPlayer` 개체.

>[!TIP]
>
>광고가 미디어에 삽입되거나 미디어에서 제거되면 TVSDK는 재생 이벤트 TimelineEvent를 전달합니다.[타임라인 업데이트됨](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| 이벤트 | 의미 |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 광고 브레이크가 완전히 재생되었습니다. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 재생 도중 광고 브레이크를 건너뛰었습니다. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 광고 브레이크가 시작되었습니다. |
| AdClickEvent.[광고 클릭(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 사용자가 광고를 클릭했습니다. 애플리케이션 호출에 대한 응답으로 사용자가 클릭한 광고에 대한 정보를 애플리케이션에 제공합니다 `notifyClick` 다음에 있음 `MediaPlayerView`. |
| AdPlaybackEvent.[광고 완료됨(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 광고가 완전히 재생되었습니다. |
| AdPlaybackEvent.[광고 진행률(_F)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 광고 재생이 진행되었습니다. 광고가 재생되는 동안 여러 번 발송되었습니다. |
| AdPlaybackEvent.[광고 찾기(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 광고 경계 간에 또는 광고 내에서 찾기가 발생했습니다. |
| AdPlaybackEvent.[광고 시작됨(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 광고가 시작되었습니다. |
