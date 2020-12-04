---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 현재 버퍼링 수준 및 사용 가능한 대역폭을 기반으로 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 현재 버퍼링 수준 및 사용 가능한 대역폭을 기반으로 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
uuid: d41c3edf-33c7-4616-820f-22303d578df0
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---


# 개요 {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 현재 버퍼링 수준 및 사용 가능한 대역폭을 기반으로 각 버스트에 대한 품질 수준을 선택할 수 있습니다.

TVSDK는 컨텐츠가 현재 네트워크 연결에 대해 최적의 비트 전송률로 재생되도록 항상 비트 전송률을 모니터링합니다. ABR(응용 비트 전송률) 전환 정책과 MBR(다중 비트 전송률) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최적의 재생 경험을 제공하는 비트 전송률로 자동 전환됩니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 속도(초당 비트 수)입니다. </p> <p>재생이 시작되면 첫 번째 세그먼트에 가장 가까운 프로파일인 초기 비트 전송률보다 크거나 같습니다. 최소 비트 전송률을 정의하고 초기 비트 전송률이 최소 비트율보다 낮은 경우 TVSDK는 최소 비트 전송률보다 낮은 비트 전송률을 갖는 프로파일을 선택합니다. 초기 비율이 최대 속도보다 높은 경우 TVSDK는 최대 속도보다 가장 높은 비율을 선택합니다. 초기 비트 전송률이 0이거나 정의되지 않은 경우 초기 비트 전송률은 ABR 정책에 의해 결정됩니다. </p> <p><span class="codeph"> get</span> ABRInitialBitRatedatory는 초당 바이트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 허용되는 가장 낮은 비트 전송률입니다. </p> <p>ABR 전환은 비트 전송률이 이 비트율보다 낮은 프로필을 무시합니다. <span class="codeph"> get</span> ABRMinBitRatetest는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. </p> <p>ABR 전환은 비트율보다 비트 속도가 높은 프로파일을 무시합니다. <span class="codeph"> get</span> ABRMaxBitRatetest는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR 전환 정책 </td> 
   <td colname="col2"> <p>재생은 가능한 경우 가장 높은 비트 전송률 프로파일로 점차 전환됩니다. ABR 전환을 위한 정책을 설정할 수 있습니다. 이 정책은 TVSDK가 프로필 간에 전환되는 속도를 결정합니다. 기본값은 <span class="codeph"> ABR_MODERATE</span>입니다. </p> <p>TVSDK가 더 높은 비트 전송률을 전환할 경우 플레이어는 현재 ABR 정책을 기반으로 전환하기 위한 이상적인 비트 전송률 프로필을 선택합니다. 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_REWARDS</span>:대역폭이 현재 비트 전송률보다 50% 높을 때 비트 전송률이 다음으로 높은 프로필로 전환합니다. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>:대역폭이 현재 비트 전송률보다 20% 높을 때 다음 높은 비트 전송률 프로파일로 전환합니다. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGAINST</span>:대역폭이 현재 비트 전송률보다 높은 경우 즉시 가장 높은 비트 전송률 프로파일로 전환됩니다. </li> 
     </ul> </p> <p>초기 비트 전송률이 0이거나 지정되지 않았지만 정책을 지정한 경우 재생은 보수 정책에 대해 가장 낮은 비트 전송률 프로필, 중간 정책에 대해 사용 가능한 프로필의 중간값 비트 비율에 가장 가까운 프로필, 공격적인 정책에 대해 가장 높은 비트 전송률 프로필로 시작합니다. </p> <p>이러한 속도가 지정된 경우 정책은 최소 및 최대 비트 전송률의 제한에서 작동합니다. </p> <p> <span class="codeph"> </span> getABRPolicyreturn the current setting from the  <span class="codeph"> </span> ABRControlParametersenum: <span class="codeph"> ABR_RESTRUCTIVE</span>,  <span class="codeph"> ABR_MODERATE</span> 또는  <span class="codeph"> ABR_EXPERATE</span>. </p> <p>자세한 내용은 ABRControlParameters API 문서를 참조하십시오.</p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 제어 매개 변수를 엄격히 준수하면서 지속적인 재생 환경을 선호하므로 TVSDK 페일오버 메커니즘이 사용자 설정을 무시할 수 있습니다.
* 비트 전송률이 변경되면 TVSDK는 `PlaybackEventListener`에서 `onProfileChanged` 이벤트를 전달합니다.

* 언제든지 ABR 설정을 변경할 수 있으며, 플레이어는 가장 최근 설정과 가장 유사한 프로파일을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있을 경우:

* 1:30000
* 2:70000
* 3:1500000
* 4:240000
* 5:4000000

300000 ~ 200000의 범위를 지정하는 경우 TVSDK는 프로파일 1, 2 및 3만 고려합니다. 이를 통해 애플리케이션은 wi-fi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 디바이스로 전환하는 등 다양한 네트워크 조건에 맞게 조정할 수 있습니다.

ABR 컨트롤 매개 변수를 설정하려면 `ABRControlParameter` 클래스에 매개 변수를 설정합니다.
