---
description: 브라우저 TVSDK는 분석 및 디버깅에 사용할 지표를 제공합니다. QoSProvider를 사용하여 이러한 측정 지표를 얻을 수 있습니다.
title: 지표
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# 지표{#metrics}

브라우저 TVSDK는 분석 및 디버깅에 사용할 지표를 제공합니다. QoSProvider를 사용하여 이러한 측정 지표를 얻을 수 있습니다.

예:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

