---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. 브라우저 TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. 브라우저 TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# 개요 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. 브라우저 TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.

브라우저 TVSDK는 컨텐츠가 현재 네트워크 연결에 적합한 비트 전송률로 재생되도록 항상 비트 전송률을 모니터링합니다.

ABR(응용 비트 전송률) 전환 정책과 MBR(다중 비트 전송률) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. 브라우저 TVSDK는 지정된 구성에서 최적의 재생 경험을 제공하는 비트 전송률로 자동 전환됩니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2">첫 번째 세그먼트에 대한 원하는 재생 비트 속도(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 가장 가까운 프로파일인 초기 비트 전송률보다 크거나 같습니다. <p> 최소 비트 전송률이 정의되고 초기 비트 전송률이 최소 비트율보다 낮은 경우 Browser TVSDK는 최소 비트 전송률보다 낮은 비트 전송률을 갖는 프로파일을 선택합니다. 초기 비율이 최대 속도보다 높은 경우 Browser TVSDK는 최대 속도보다 가장 높은 비율을 선택합니다. </p> <p>초기 비트 전송률이 0이거나 정의되지 않은 경우 초기 비트 전송률은 ABR 정책에 의해 결정됩니다. </p> <p><span class="codeph"> </span> initialBitRatepoint는 초당 바이트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2">ABR이 전환할 수 있는 허용되는 가장 낮은 비트 전송률입니다. ABR 전환은 비트 전송률이 이 비트율보다 낮은 프로필을 무시합니다. <p><span class="codeph"> </span> minBitRatetest는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2">ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환은 비트율보다 비트 속도가 높은 프로파일을 무시합니다. <p><span class="codeph"> </span> maxBitRatetest는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* 비트 전송률이 변경되면 Browser TVSDK는 `AdobePSDK.ProfileEvent` 유형으로 `AdobePSDK.PSDKEventType.PROFILE_CHANGED`을 전달합니다.

* 언제든지 ABR 설정을 변경할 수 있으며, 플레이어는 가장 최근 설정과 가장 유사한 프로파일을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있을 경우:

* 1:30000
* 2:70000
* 3:1500000
* 4:240000
* 5:4000000

300000 ~ 200000의 범위를 지정하는 경우 브라우저 TVSDK는 프로파일 1, 2 및 3만 고려합니다. 이를 통해 애플리케이션은 wi-fi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 디바이스로 전환하는 등 다양한 네트워크 조건에 맞게 조정할 수 있습니다.

ABR 제어 매개 변수를 설정하려면

* `ABRControlParameters` 클래스에 매개 변수를 설정합니다.

