---
description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-description: QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹
seo-title: 서비스 품질 통계
title: 서비스 품질 통계
uuid: c08c1031-616a-4776-92e2-1c405467689b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 서비스 품질 통계 {#quality-of-service-statistics}

QoS(Quality of Service)는 비디오 엔진의 성능을 자세히 보여줍니다. TVSDK 파섹

## QOS 재생, 버퍼링 및 디바이스 통계 읽기 {#section_9996406E2D814FA382B77E3041CB02BC}

재생, 버퍼링 및 장치 통계를 `PTQOSProvider` 클래스에서 읽을 수 있습니다.

이 `PTQOSProvider` 클래스는 버퍼링, 비트 속도, 프레임 속도, 시간 데이터 등에 대한 정보를 비롯한 다양한 통계를 제공합니다.

또한 모델, 운영 체제 및 제조업체 장치 ID와 같은 장치에 대한 정보도 제공합니다.

>[!TIP]
>
>재생 버퍼 크기는 변경할 수 없지만 디버깅 또는 분석을 위해 버퍼 크기 상태를 모니터링할 수 있습니다. `PTPlaybackInformation` 에는 `playbackBufferFull` 및 와 같은 속성이 `playbackLikelyToKeepUp`포함됩니다.

1. 미디어 플레이어를 인스턴스화합니다.
1. 개체를 `PTQOSProvider` 만들어 미디어 플레이어에 연결합니다.

   생성자는 장치별 정보를 검색할 수 있도록 플레이어 컨텍스트를 받습니다. `PTQOSProvider`

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (선택 사항) 재생 통계를 확인합니다.

   재생 통계를 읽을 수 있는 한 가지 방법은 타이머와 같은 타이머를 갖는 `NSTimer`것입니다. 이 타이머는 에서 새로운 QoS 값을 주기적으로 가져옵니다 `PTQOSProvider`. 예:

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. (선택 사항) 장치별 정보를 확인합니다.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
