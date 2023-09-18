---
description: 재생에 광고가 포함되는 경우 TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.
title: 광고 이벤트 순서
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 광고 이벤트 순서{#order-of-advertising-events}

재생에 광고가 포함되는 경우 TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* 다음은 광고 브레이크의 모든 광고에 대해 발송됩니다.

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (광고 재생 중 여러 번)
   * `AdClickEvent.AD_CLICK` (클릭할 때마다)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

다음 예는 광고 재생 이벤트의 일반적인 진행률을 보여 줍니다.

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
