---
description: 브라우저 TVSDK는 분석 및 디버깅에 사용할 지표를 제공합니다. QoSProvider를 사용하여 이러한 지표를 가져올 수 있습니다.
title: 지표
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 지표{#metrics}

브라우저 TVSDK는 분석 및 디버깅에 사용할 지표를 제공합니다. QoSProvider를 사용하여 이러한 지표를 가져올 수 있습니다.

예:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
