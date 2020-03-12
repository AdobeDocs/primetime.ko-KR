---
description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. Browser TVSDK는 재생, 버퍼링 및 디바이스에 대한 자세한 통계를 제공합니다.
seo-description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. Browser TVSDK는 재생, 버퍼링 및 디바이스에 대한 자세한 통계를 제공합니다.
seo-title: 서비스 품질 통계
title: 서비스 품질 통계
uuid: e4bb2617-d8a7-4da7-b669-d6ffab2864bb
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 서비스 품질 통계{#quality-of-service-statistics}

QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. Browser TVSDK는 재생, 버퍼링 및 디바이스에 대한 자세한 통계를 제공합니다.

## QOS 재생, 버퍼링 및 디바이스 통계 읽기 {#read-qos-playback-buffering-and-device-statistics}

QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.

이 `QOSProvider` 클래스는 버퍼링, 비트 속도, 프레임 속도, 시간 데이터 등에 대한 정보를 비롯한 다양한 통계를 제공합니다.

1. 미디어 플레이어를 인스턴스화합니다.
1. 개체를 `QOSProvider` 만들어 미디어 플레이어에 연결합니다.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (선택 사항) 재생 통계를 확인합니다.

   재생 통계를 읽을 수 있는 한 가지 방법은 타이머를 갖는 것입니다. 타이머를 사용하면 타이머에서 새로운 QoS 값을 정기적으로 가져올 수 `QOSProvider`있습니다. 예:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. (선택 사항) 장치별 정보를 확인합니다.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
