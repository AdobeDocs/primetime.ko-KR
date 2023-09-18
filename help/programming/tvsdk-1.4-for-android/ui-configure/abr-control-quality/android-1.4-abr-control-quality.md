---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.
title: 비디오 품질을 위한 적응형 비트 전송률(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 개요 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.

TVSDK는 비트 전송률을 지속적으로 모니터링하여 콘텐츠가 현재 네트워크 연결에 대한 최적의 비트 전송률로 재생되도록 합니다.

ABR(Adaptive Bit-rate) 스위칭 정책과 다중 비트 전송률(MBR) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최상의 재생 환경을 제공하는 비트 전송률로 자동으로 전환합니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 전송률(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 초기 비트 전송률과 같거나 더 큰 가장 가까운 프로파일이 사용됩니다. </p> <p> 최소 비트율이 정의되어 있고, 초기 비트율이 최소 비트율보다 낮으면, TVSDK는 최소 비트율보다 가장 낮은 비트율을 갖는 프로파일을 선택한다. 초기 비율이 최대 비율보다 높으면 TVSDK는 최대 비율보다 낮은 가장 높은 비율을 선택합니다. </p> <p>초기 비트 레이트가 0이거나 정의되지 않은 경우, 초기 비트 레이트는 ABR 정책에 의해 결정된다. </p> <p><span class="codeph"> getABRInitialBitRate</span> 초당 바이트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 낮은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 낮은 비트 전송률의 프로파일을 무시합니다. </p> <p><span class="codeph"> getABRMinBitRate</span> 초당 비트 수를 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 높은 비트 전송률을 사용하는 프로파일이 무시됩니다. </p> <p><span class="codeph"> getABRMaxBitRate</span> 초당 비트 수를 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR 전환 정책 </td> 
   <td colname="col2"> 가능한 경우 재생은 가장 높은 비트 전송률 프로필로 점진적으로 전환됩니다. TVSDK가 프로필 간에 전환하는 속도를 결정하는 ABR 전환에 대한 정책을 설정할 수 있습니다. 기본값은 입니다 <span class="codeph"> ABR_MODERATE</span>. <p>TVSDK가 더 높은 비트 전송률로 전환하기로 결정하면 플레이어는 현재 ABR 정책에 따라 전환할 이상적인 비트 전송률 프로필을 선택합니다. 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: 대역폭이 현재 비트 전송률보다 50% 높으면 비트 전송률이 다음으로 높은 프로파일로 전환합니다. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: 대역폭이 현재 비트 전송률보다 20% 더 높을 때 다음으로 높은 비트 전송률 프로필로 전환합니다. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: 대역폭이 현재 비트율보다 높을 때 가장 높은 비트율 프로파일로 즉시 전환합니다. </li> 
     </ul> </p> <p>초기 비트 전송률이 0이거나 지정되지 않았지만 정책이 지정된 경우, 재생은 보존에 대한 가장 낮은 비트 전송률 프로필, 보통에 대한 사용 가능한 프로필의 중간 비트 전송률에 가장 가까운 프로필 및 공격성에 대한 가장 높은 비트 전송률 프로필로 시작됩니다. </p> <p>이 속도들이 지정된다면, 이 정책은 최소 및 최대 비트 속도들의 제약들 내에서 작동한다. </p> <p><span class="codeph"> getABRPolicy</span> 에서 현재 설정을 반환합니다. <span class="codeph"> ABRControlParameters</span> 열거형: 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_CONSERVATIVE</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MODERATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_AGGRESSIVE</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 제어 매개 변수를 엄격히 준수하는 것보다 지속적인 재생 환경을 선호하므로 TVSDK 장애 조치(failover) 메커니즘이 사용자의 설정을 재정의할 수 있습니다.
* 비트 전송률이 변경되면 TVSDK가 발송됩니다. `onProfileChanged` 의 이벤트 `PlaybackEventListener`.

* 언제든지 ABR 설정을 변경할 수 있으며 플레이어는 최신 설정과 가장 일치하는 프로필을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있는 경우:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

300000~2000000 범위를 지정하면 TVSDK는 프로필 1, 2 및 3만 고려합니다. 이를 통해 응용 프로그램은 Wi-Fi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 장치로 전환하는 등 다양한 네트워크 조건에 적응할 수 있습니다.

ABR 컨트롤 매개 변수를 설정하려면 `ABRControlParameter` 클래스.
