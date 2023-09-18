---
description: 브라우저 TVSDK는 QoS(서비스 품질) 이벤트를 발송하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.
title: QoS 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# QoS 이벤트{#qos-events}

브라우저 TVSDK는 QoS(서비스 품질) 이벤트를 발송하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 의 인스턴스를 만듭니다. `AdobePSDK.QOSProvider` 여기에 MediaPlayer 인스턴스 연결 `QOSProvider` 인스턴스:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

응용 프로그램에서 타이머를 구성하여 `playbackInformation` 의 속성 `qosProvider` 인스턴스. 다음 `playbackInformation` 속성은 현재 재생 통계의 스냅샷을 제공합니다. 예:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
