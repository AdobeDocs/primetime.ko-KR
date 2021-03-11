---
description: 브라우저 TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
title: QoS 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# QoS 이벤트{#qos-events}

브라우저 TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 `AdobePSDK.QOSProvider` 인스턴스를 만들고 이 `QOSProvider` 인스턴스에 MediaPlayer 인스턴스를 연결하십시오.

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

응용 프로그램에서 타이머를 구성하여 `qosProvider` 인스턴스의 `playbackInformation` 속성을 정기적으로 확인합니다. `playbackInformation` 속성은 현재 재생 통계의 스냅숏을 제공합니다. 예:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

