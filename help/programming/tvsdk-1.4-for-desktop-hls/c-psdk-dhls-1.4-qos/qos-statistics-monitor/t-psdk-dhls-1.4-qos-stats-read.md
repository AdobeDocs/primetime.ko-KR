---
description: QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.
title: QOS 재생, 버퍼링 및 장치 통계 읽기
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# QOS 재생, 버퍼링 및 장치 통계 읽기{#read-qos-playback-buffering-and-device-statistics}

QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.

다음 `QOSProvider` 클래스는 버퍼링, 비트 전송률, 프레임 속도, 시간 데이터 등에 대한 정보를 포함하여 다양한 통계를 제공합니다.

또한 제조업체, 모델, 운영 체제, SDK 버전 및 화면 크기/밀도와 같은 디바이스에 대한 정보도 제공합니다.

1. 미디어 플레이어 인스턴스화.
1. 만들기 `QOSProvider` 개체를 복사하여 미디어 플레이어에 첨부합니다.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (선택 사항) 재생 통계를 읽습니다.

   재생 통계를 읽는 한 가지 솔루션은 타이머를 갖는 것입니다. 이 타이머는 주기적으로 `QOSProvider`. 예:

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

1. (선택 사항) 장치별 정보를 읽습니다.

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

