---
description: 브라우저 TVSDK 파섹 QoSProvider를 사용하여 이러한 지표를 얻을 수 있습니다.
seo-description: 브라우저 TVSDK 파섹 QoSProvider를 사용하여 이러한 지표를 얻을 수 있습니다.
seo-title: 지표
title: 지표
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 지표{#metrics}

브라우저 TVSDK 파섹 QoSProvider를 사용하여 이러한 지표를 얻을 수 있습니다.

예:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

