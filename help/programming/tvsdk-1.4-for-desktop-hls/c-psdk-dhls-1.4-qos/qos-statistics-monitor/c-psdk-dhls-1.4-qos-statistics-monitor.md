---
description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-title: 서비스 품질 통계
title: 서비스 품질 통계
uuid: 5c9d09a9-0e0b-44f2-98ca-2eeb8a830ec6
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 서비스 품질 통계 {#quality-of-service-statistics}

QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹

TVSDK는 다음과 같은 다운로드 리소스에 대한 정보도 제공합니다.

* 재생 목록/매니페스트 파일
* 파일 조각
* 파일에 대한 추적 정보

## 로드 정보를 사용하여 조각 수준에서 추적 {#track-at-the-fragment-level-using-load-information}

LoadInformation 클래스에서 조각 및 트랙과 같은 다운로드한 리소스에 대한 QoS(서비스 품질) 정보를 읽을 수 있습니다.

1. 콜백 이벤트 리스너를 `onLoadInformationAvailable` 구현합니다.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 조각을 다운로드할 때마다 TVSDK가 호출하는 이벤트 리스너를 등록합니다.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 콜백으로 전달되는 `LoadInformation` 파일의 관심 데이터를 읽습니다.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 속성 </th> 
      <th colname="col1" class="entry"> 유형 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> <p>다운로드 지속 시간(밀리초)입니다. </p> <p>TVSDK는 클라이언트가 서버에 연결하는 데 걸린 시간과 전체 조각을 다운로드하는 데 걸린 시간을 구별하지 않습니다. 예를 들어 10MB 세그먼트를 다운로드하는 데 8초가 걸리는 경우 TVSDK는 해당 정보를 제공하지만 첫 번째 바이트가 될 때까지 4초, 전체 조각을 다운로드하는 데 4초가 걸렸다고 알려주지 않습니다. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> 다운로드한 조각의 미디어 지속 시간(밀리초)입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 크기 </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> 다운로드한 리소스의 크기(바이트)입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 해당 트랙의 색인(알려진 경우)그렇지 않으면 0입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 해당 트랙의 이름(알려진 경우)그렇지 않으면 null입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 해당 트랙의 유형(알려진 경우)그렇지 않으면 null입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 다운로드한 TVSDK 다음 중 하나: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - 재생 목록/매니페스트 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">조각 - 조각 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - 특정 트랙과 연결된 조각 </li> 
      </ul> 리소스 유형을 감지할 수 없는 경우가 있습니다. 이 경우 FILE이 반환됩니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 다운로드한 리소스를 가리키는 URL입니다. </td> 
   </tr> 
   </tbody> 
   </table>

## QOS 재생, 버퍼링 및 디바이스 통계 읽기 {#read-qos-playback-buffering-and-device-statistics}

QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.

이 `QOSProvider` 클래스는 버퍼링, 비트 속도, 프레임 속도, 시간 데이터 등에 대한 정보를 비롯한 다양한 통계를 제공합니다.

제조업체, 모델, 운영 체제, SDK 버전 및 화면 크기/밀도와 같은 장치에 대한 정보도 제공합니다.

1. 미디어 플레이어를 인스턴스화합니다.
1. 개체를 `QOSProvider` 만들어 미디어 플레이어에 연결합니다.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (선택 사항) 재생 통계를 확인합니다.

   재생 통계를 읽을 수 있는 한 가지 방법은 타이머를 갖는 것입니다. 타이머를 사용하면 타이머에서 새로운 QoS 값을 정기적으로 가져올 수 `QOSProvider`있습니다. 예:

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

1. (선택 사항) 장치별 정보를 확인합니다.

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
