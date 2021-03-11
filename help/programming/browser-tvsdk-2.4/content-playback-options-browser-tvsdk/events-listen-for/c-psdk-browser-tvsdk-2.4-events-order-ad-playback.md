---
description: 재생에 광고가 포함되는 경우 Browser TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
title: 광고 이벤트 순서
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 광고 이벤트 순서{#order-of-advertising-events}

재생에 광고가 포함되는 경우 Browser TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 광고 노출의 모든 광고에 대해 다음 사항이 전달됩니다.

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (광고를 재생하는 동안 여러 번)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

다음 예는 광고 재생 이벤트의 일반적인 진행 상태를 보여줍니다.

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

