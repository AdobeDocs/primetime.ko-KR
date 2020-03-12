---
description: Browser TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.
seo-description: Browser TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.
seo-title: QoS 이벤트
title: QoS 이벤트
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# QoS 이벤트{#qos-events}

Browser TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트에 대해 애플리케이션에 알립니다.

모든 QoS 관련 이벤트에 대한 알림을 받으려면 MediaPlayer 인스턴스를 `AdobePSDK.QOSProvider` 만들고 이 `QOSProvider` 인스턴스에 연결하십시오.

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

애플리케이션에서 타이머를 구성하여 인스턴스의 `playbackInformation` 속성을 주기적으로 확인합니다 `qosProvider` . 이 `playbackInformation` 속성은 현재 재생 통계의 스냅숏을 제공합니다. 예:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

