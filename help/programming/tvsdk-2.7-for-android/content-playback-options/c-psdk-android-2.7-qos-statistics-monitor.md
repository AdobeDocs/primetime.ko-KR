---
description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-title: 서비스 품질 통계
title: 서비스 품질 통계
uuid: 8e990461-065b-4efa-b77c-b2b832f86f7d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 서비스 품질 통계 {#quality-of-service-statistics}

QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹

TVSDK는 다음과 같은 다운로드 리소스에 대한 정보도 제공합니다.

* 재생 목록/매니페스트 파일
* 파일 조각
* 파일에 대한 추적 정보

## 로드 정보를 사용하여 조각 수준에서 추적 {#section_4439D91E8EDC45588EF1D7BE25697350}

조각이나 트랙과 같은 다운로드한 리소스에 대한 QoS(서비스 품질) 정보를 `LoadInformation` 클래스에서 읽을 수 있습니다.

1. 이벤트 리스너를 구현하고 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 등록합니다.
1. 콜백을 `event.getLoadInformation()` 호출하여 콜백으로 전달되는 `event` 매개 변수에서 관련 데이터를 읽습니다.

   >[!NOTE]
   >
   >자세한 `LoadInformation`내용은 Android용 [2.7(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API 문서를 참조하십시오.

## QOS 재생, 버퍼링 및 디바이스 통계 읽기 {#section_D21722600F324E67A9F06234D338B243}

재생, 버퍼링 및 장치 통계를 `QOSProvider` 클래스에서 읽을 수 있습니다.

이 `QOSProvider` 클래스는 버퍼링, 비트 속도, 프레임 속도, 시간 데이터 등에 대한 정보를 비롯한 다양한 통계를 제공합니다. 제조업체, 모델, 운영 체제, SDK 버전, 제조업체 장치 ID, 화면 크기/밀도 등 장치에 대한 정보도 제공합니다.

1. 미디어 플레이어를 인스턴스화합니다.
1. 개체를 `QOSProvider` 만들어 미디어 플레이어에 연결합니다.

   생성자는 장치별 정보를 검색할 수 있도록 플레이어 컨텍스트를 받습니다. `QOSProvider`

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (선택 사항) 재생 통계를 확인합니다.

   재생 통계를 읽을 수 있는 한 가지 방법은 타이머를 갖는 것입니다. 타이머를 사용하면 타이머에서 새로운 QoS 값을 정기적으로 가져올 수 `QOSProvider`있습니다.

   예:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. (선택 사항) 장치별 정보를 확인합니다.

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```

