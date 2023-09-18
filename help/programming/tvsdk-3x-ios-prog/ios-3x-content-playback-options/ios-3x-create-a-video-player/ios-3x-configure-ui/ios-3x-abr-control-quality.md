---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.
title: 비디오 품질을 위한 적응형 비트 전송률(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 비디오 품질을 위한 적응형 비트 전송률(ABR) {#adaptive-bit-rates-abr-for-video-quality}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.

TVSDK는 비트 전송률을 지속적으로 모니터링하여 콘텐츠가 현재 네트워크 연결에 대한 최적의 비트 전송률로 재생되도록 합니다.

ABR(Adaptive Bit-rate) 스위칭 정책과 다중 비트 전송률(MBR) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최상의 재생 환경을 제공하는 비트 전송률로 자동으로 전환합니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 전송률(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 초기 비트 전송률과 같거나 더 큰 가장 가까운 프로파일이 사용됩니다. </p> <p> 최소 비트율이 정의되어 있고, 초기 비트율이 최소 비트율보다 낮으면, TVSDK는 최소 비트율보다 가장 낮은 비트율을 갖는 프로파일을 선택한다. 초기 비율이 최대 비율보다 높으면 TVSDK는 최대 비율보다 낮은 가장 높은 비율을 선택합니다. </p> <p>초기 비트 레이트가 0이거나 정의되지 않은 경우, 초기 비트 레이트는 ABR 정책에 의해 결정된다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 낮은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 낮은 비트 전송률의 프로파일을 무시합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 높은 비트 전송률을 사용하는 프로파일이 무시됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 비트 전송률 전환에서 이벤트를 발송하지 않습니다.
* 언제든지 ABR 설정을 변경할 수 있으며 플레이어는 최신 설정과 가장 일치하는 프로필을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있는 경우:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

300000~2000000 범위를 지정하면 TVSDK는 프로필 1, 2 및 3만 고려합니다. 이를 통해 응용 프로그램은 WiFi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 장치로 전환하는 등 다양한 네트워크 조건에 적응할 수 있습니다.

## 적응형 비트 전송률 구성 {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

TVSDK 적응형 비트 전송률 매개 변수를 구성하려면:

1. 의 인스턴스 구성 `PTABRControlParameters` 초기, 최소 및 최대 비트 전송률 설정을 지정합니다.

   기본값은 다음 코드 조각에 표시되지만, 응용 프로그램에서 이러한 각 매개 변수에 대해 정수 값을 설정할 수 있습니다.

   >[!IMPORTANT]
   >
   >비트 전송률 설정을 bps(bits-per-second)로 지정합니다.

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. 업데이트 `PTMediaPlayer` 가 구성된 인스턴스 `PTABRControlParameters` 인스턴스.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

다음 사항을 기억하십시오.

* 애플리케이션은 다음을 설정해야 합니다. `abrControlParameters` 속성 `PTMediaPlayer` 을(를) 구성하기 전에 `PTMediaPlayerItem` 적용할 초기 및 최소 비트율 설정에 대한 인스턴스입니다.

  컨텐츠 재생이 시작된 후 새 인스턴스를 설정하면 최대 비트율 설정에만 영향을 줍니다.

* 재생 중에 최대 비트율 설정을 업데이트하려면 새 를 만듭니다 `PTABRControlParameters` 인스턴스를 설정하고 플레이어 인스턴스에 설정합니다.
* iOS 8.0 이상에서만 재생 중 최대 비트율 설정을 업데이트할 수 있습니다. 이전 버전의 경우 `maxBitrate` 컨텐츠 재생이 시작되기 전에 설정된 값이 사용됩니다.
