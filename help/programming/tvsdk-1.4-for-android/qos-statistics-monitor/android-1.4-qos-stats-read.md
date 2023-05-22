---
description: QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.
title: QOS 재생, 버퍼링 및 장치 통계 읽기
exl-id: 1b79c254-4135-4d77-8b24-473f214021a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# QOS 재생, 버퍼링 및 장치 통계 읽기{#read-qos-playback-buffering-and-device-statistics}

QOSProvider 클래스에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다.

다음 `QOSProvider` 클래스는 버퍼링, 비트 전송률, 프레임 속도, 시간 데이터 등에 대한 정보를 포함하여 다양한 통계를 제공합니다.

또한 제조업체, 모델, 운영 체제, SDK 버전, 제조업체의 디바이스 ID 및 화면 크기/밀도와 같은 디바이스에 대한 정보도 제공합니다.

1. 미디어 플레이어 인스턴스화.
1. 만들기 `QOSProvider` 개체를 복사하여 미디어 플레이어에 첨부합니다.

   다음 `QOSProvider` 생성자는 장치별 정보를 검색할 수 있도록 플레이어 컨텍스트를 사용합니다.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (선택 사항) 재생 통계를 읽습니다.

   재생 통계를 읽는 한 가지 솔루션은 타이머를 갖는 것입니다. 이 타이머는 주기적으로 `QOSProvider`. 예:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation = _mediaQosProvider.getPlaybackInformation();  
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

1. (선택 사항) 장치별 정보를 읽습니다.

   ```java
   // Show device information 
   DeviceInformation deviceInfo =  
     new QOSProvider(parent.getApplicationContext()).getDeviceInformation(); 
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
