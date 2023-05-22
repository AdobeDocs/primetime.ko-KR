---
description: 재생에 광고가 포함되는 경우 브라우저 TVSDK는 일반적으로 예상되는 순서로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.
title: 광고 이벤트 순서
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 광고 이벤트 순서{#order-of-advertising-events}

재생에 광고가 포함되는 경우 브라우저 TVSDK는 일반적으로 예상되는 순서로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 다음은 광고 브레이크의 모든 광고에 대해 발송됩니다.

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (광고 재생 중 여러 번)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

다음 예는 광고 재생 이벤트의 일반적인 진행률을 보여 줍니다.

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
