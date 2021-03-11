---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 사용 가능한 대역폭에 따라 각 버스트의 품질 수준을 선택할 수 있습니다.
title: 비디오 품질을 위한 적응형 비트 전송률(ABR)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# 비디오 품질에 대한 응용 비트 전송률(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 사용 가능한 대역폭에 따라 각 버스트의 품질 수준을 선택할 수 있습니다.

TVSDK는 컨텐츠가 현재 네트워크 연결에 대해 최적의 비트 전송률로 재생되도록 항상 비트 전송률을 모니터링합니다.

ABR(응용 비트 전송률) 전환 정책과 MBR(다중 비트 전송률) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최적의 재생 경험을 제공하는 비트 전송률로 자동 전환됩니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 전송률(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 대해 첫 번째 비트율보다 크거나 같은 가장 가까운 프로필이 사용됩니다. </p> <p> 최소 비트 전송률이 정의되고 초기 비트 전송률이 최소 비트율보다 낮은 경우 TVSDK는 최소 비트 전송률보다 낮은 비트 전송률을 갖는 프로파일을 선택합니다. 초기 비율이 최대 속도보다 높은 경우 TVSDK는 최대 속도보다 가장 높은 비율을 선택합니다. </p> <p>초기 비트 전송률이 0이거나 정의되지 않은 경우 초기 비트 전송률은 ABR 정책에 의해 결정됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 허용되는 가장 낮은 비트 전송률입니다. ABR 전환은 이 비트 전송률보다 낮은 비트 전송률의 프로파일을 무시합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환은 비트 전송률이 이 비트율보다 높은 프로파일을 무시합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 비트 전송률 전환으로 이벤트를 전달하지 않습니다.
* 언제든지 ABR 설정을 변경할 수 있으며 가장 최근 설정과 가장 유사한 프로파일을 사용하도록 플레이어가 전환됩니다.

예를 들어 스트림에 다음 프로필이 있을 경우:

* 1:300000
* 2:700000
* 3:1500000
* 4:2400000
* 5:4000000

300,000 ~ 2000000 범위를 지정하는 경우 TVSDK는 프로파일 1, 2 및 3만 고려합니다. 이를 통해 애플리케이션은 WiFi에서 3G로 전환하는 등 다양한 네트워크 조건에 맞게 조정하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 디바이스로 전환할 수 있습니다.

## 응용 비트 전송률 구성 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

TVSDK 적응형 비트 전송률 매개 변수를 구성하려면:

1. 초기, 최소 및 최대 비트 전송률 설정을 설정하려면 `PTABRControlParameters` 인스턴스를 구성합니다.

   기본값은 다음 코드 조각에 표시되지만 응용 프로그램은 이러한 각 매개 변수에 대해 정수 값을 설정할 수 있습니다.

   >[!IMPORTANT]
   >
   >비트 전송률 설정을 비트/초(bps)로 지정합니다.

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 구성된 `PTABRControlParameters` 인스턴스로 `PTMediaPlayer` 인스턴스를 업데이트합니다.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

다음 사항을 기억하십시오.

* 초기 및 최소 비트 전송률 설정이 적용되도록 `PTMediaPlayerItem` 인스턴스를 구성하려면 먼저 `PTMediaPlayer`에 `abrControlParameters` 속성을 설정해야 합니다.

   컨텐츠 재생이 시작되면 새 인스턴스를 설정하면 최대 비트 전송률 설정에만 영향을 미칩니다.

* 재생 중에 최대 비트 전송률 설정을 업데이트하려면 새 `PTABRControlParameters` 인스턴스를 만들고 플레이어 인스턴스에서 설정합니다.
* iOS 8.0 이상에서만 재생되는 동안 최대 비트 전송률 설정을 업데이트할 수 있습니다. 이전 버전의 경우 내용 재생이 시작되기 전에 설정된 `maxBitrate` 값이 사용됩니다.

