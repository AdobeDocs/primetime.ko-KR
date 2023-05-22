---
description: 브라우저 TVSDK는 분석 및 디버깅에 사용할 지표를 제공합니다. QoSProvider를 사용하여 이러한 지표를 가져올 수 있습니다.
title: 지표
exl-id: 1413ddf5-b458-4040-abf8-8d9dbd6b80e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
