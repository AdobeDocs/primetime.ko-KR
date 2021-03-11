---
description: TVSDK는 광고 재생이 시작되는 시기 등 광고 관련 작업에 대한 응답으로 광고 재생 이벤트를 전달합니다.
title: 광고 재생 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# 광고 재생 이벤트 {#ad-playback-events}

TVSDK는 광고 재생이 시작되는 시기 등 광고 관련 작업에 대한 응답으로 광고 재생 이벤트를 전달합니다.

모든 광고 재생 관련 이벤트에 대한 알림을 받으려면 다음 이벤트에 대해 `MediaPlayer` 객체에 리스너를 등록합니다.

>[!TIP]
>
>광고가 미디어에 삽입되거나 미디어에서 제거되면 TVSDK는 재생 이벤트 TimelineEvent를 전달합니다.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| 이벤트 | 의미 |
|---|---|
| AdBreakPlaybackEvent를 참조하십시오.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 광고 브레이크가 완전히 열렸다. |
| AdBreakPlaybackEvent를 참조하십시오.[AD_BREAK_OVERSEED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 재생하는 동안 광고 나누기를 건너뛰었습니다. |
| AdBreakPlaybackEvent를 참조하십시오.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 광고 중단이 시작되었습니다. |
| AdClickEvent를 참조하십시오.[광고 클릭(_R)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 사용자가 광고를 클릭했습니다. 응용 프로그램에서 `MediaPlayerView`에서 `notifyClick`을(를) 호출하는 응답으로 사용자가 클릭한 광고에 대한 정보를 응용 프로그램에 제공합니다. |
| AdPlaybackEvent를 참조하십시오.[광고 완료(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 광고가 완전히 나왔다. |
| AdPlaybackEvent를 참조하십시오.[광고 진행률(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 광고 재생이 더욱 빨라졌습니다. 광고가 재생되는 동안 여러 번 전달됩니다. |
| AdPlaybackEvent를 참조하십시오.[광고 검색(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 광고 경계 또는 광고 내에서 검색이 발생했습니다. |
| AdPlaybackEvent를 참조하십시오.[광고 시작(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 광고가 시작되었습니다. |