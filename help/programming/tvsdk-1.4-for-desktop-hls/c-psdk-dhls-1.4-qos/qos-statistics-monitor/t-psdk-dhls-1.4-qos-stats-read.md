---
description: QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.
seo-description: QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.
seo-title: QOS 재생, 버퍼링 및 디바이스 통계 읽기
title: QOS 재생, 버퍼링 및 디바이스 통계 읽기
uuid: 5ee631fc-cd6f-4f35-8621-2ffdc51a57c7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# QOS 재생, 버퍼링 및 디바이스 통계 읽기{#read-qos-playback-buffering-and-device-statistics}

QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.

`QOSProvider` 클래스는 버퍼링, 비트 속도, 프레임 속도, 시간 데이터 등에 대한 정보를 포함하여 다양한 통계를 제공합니다.

또한 제조업체, 모델, 운영 체제, SDK 버전 및 화면 크기/밀도와 같은 장치에 대한 정보도 제공합니다.

1. 미디어 플레이어를 인스턴스화합니다.
1. `QOSProvider` 개체를 만들어 미디어 플레이어에 연결합니다.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (선택 사항) 재생 통계를 확인합니다.

   재생 통계를 읽는 한 가지 방법은 타이머를 갖는 것입니다. 타이머는 정기적으로 `QOSProvider`에서 새로운 QoS 값을 가져옵니다. 예:

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (선택 사항) 디바이스별 정보를 확인합니다.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```

