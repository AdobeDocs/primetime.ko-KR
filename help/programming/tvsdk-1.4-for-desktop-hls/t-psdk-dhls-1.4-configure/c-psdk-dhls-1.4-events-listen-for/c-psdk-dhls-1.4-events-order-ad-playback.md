---
description: 재생에 광고가 포함되면 TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-description: 재생에 광고가 포함되면 TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-title: 광고 이벤트 순서
title: 광고 이벤트 순서
uuid: 34a6a606-2f2e-42de-88fd-c91202cafddf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 광고 이벤트 순서{#order-of-advertising-events}

재생에 광고가 포함되면 TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* 광고 중단의 모든 광고에 대해 다음이 전달됩니다.

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (광고를 재생하는 동안 여러 번)
   * `AdClickEvent.AD_CLICK` (for each click)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

다음 예는 광고 재생 이벤트의 일반적인 진행 상태를 보여줍니다.

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```

