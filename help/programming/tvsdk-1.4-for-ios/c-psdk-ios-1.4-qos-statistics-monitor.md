---
description: QoS(서비스 품질)는 비디오 엔진이 수행되는 방식에 대한 세부 보기를 제공합니다. TVSDK는 재생, 버퍼링 및 장치에 대한 자세한 통계를 제공합니다.
title: 서비스 품질 통계
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 서비스 품질 통계{#quality-of-service-statistics}

QoS(서비스 품질)는 비디오 엔진이 수행되는 방식에 대한 세부 보기를 제공합니다. TVSDK는 재생, 버퍼링 및 장치에 대한 자세한 통계를 제공합니다.

## QOS 재생, 버퍼링 및 장치 통계 읽기 {#section_9996406E2D814FA382B77E3041CB02BC}

에서 재생, 버퍼링 및 장치 통계를 읽을 수 있습니다. `PTQOSProvider` 클래스.

다음 `PTQOSProvider` 클래스는 버퍼링, 비트 전송률, 프레임 속도, 시간 데이터 등에 대한 정보를 포함하여 다양한 통계를 제공합니다.

또한 모델, 운영 체제 및 제조업체의 장치 ID와 같은 장치에 대한 정보도 제공합니다.

>[!TIP]
>
>재생 버퍼 크기를 변경할 수 없지만 디버깅이나 분석을 위해 버퍼 크기의 상태를 모니터링할 수 있습니다. `PTPlaybackInformation` 다음과 같은 속성을 포함합니다. `playbackBufferFull` 및 `playbackLikelyToKeepUp`.

1. 미디어 플레이어 인스턴스화.
1. 만들기 `PTQOSProvider` 개체를 복사하여 미디어 플레이어에 첨부합니다.

   다음 `PTQOSProvider` 생성자는 장치별 정보를 검색할 수 있도록 플레이어 컨텍스트를 사용합니다.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (선택 사항) 재생 통계를 읽습니다.

   재생 통계를 읽는 한 가지 솔루션은 다음과 같은 타이머를 사용하는 것입니다. `NSTimer`에서 정기적으로 새 QoS 값을 가져옵니다. `PTQOSProvider`. 예:

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

1. (선택 사항) 장치별 정보를 읽습니다.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
