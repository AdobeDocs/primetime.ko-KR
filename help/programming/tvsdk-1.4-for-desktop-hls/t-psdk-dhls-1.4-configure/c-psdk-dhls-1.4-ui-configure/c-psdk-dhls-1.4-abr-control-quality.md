---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.
title: 비디오 품질을 위한 적응형 비트 전송률(ABR)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 비디오 품질을 위한 적응형 비트 전송률(ABR){#adaptive-bit-rates-abr-for-video-quality}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 상이한 비트 레이트 인코딩(프로필)을 제공한다. TVSDK는 가용 대역폭에 기초하여 각 버스트에 대한 품질 레벨을 선택할 수 있다.

TVSDK는 비트 전송률을 지속적으로 모니터링하여 콘텐츠가 현재 네트워크 연결에 대한 최적의 비트 전송률로 재생되도록 합니다.

ABR(Adaptive Bit-rate) 스위칭 정책과 다중 비트 전송률(MBR) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최상의 재생 환경을 제공하는 비트 전송률로 자동으로 전환합니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 전송률(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 초기 비트 전송률과 같거나 더 큰 가장 가까운 프로파일이 사용됩니다. </p> <p> 최소 비트율이 정의되어 있고, 초기 비트율이 최소 비트율보다 낮으면, TVSDK는 최소 비트율보다 가장 낮은 비트율을 갖는 프로파일을 선택한다. 초기 비율이 최대 비율보다 높으면 TVSDK는 최대 비율보다 낮은 가장 높은 비율을 선택합니다. </p> <p>초기 비트 레이트가 0이거나 정의되지 않은 경우, 초기 비트 레이트는 ABR 정책에 의해 결정된다. </p> <p> <span class="apiname"> ABRInitialBitRate </span> 초당 바이트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 낮은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 낮은 비트 전송률의 프로파일을 무시합니다. </p> <p> <span class="apiname"> ABRMinBitRate </span> 초당 비트 수를 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환에서는 이 비트 전송률보다 높은 비트 전송률을 사용하는 프로파일이 무시됩니다. </p> <p> <span class="apiname"> ABRMaxBitRate </span> 초당 비트 수를 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR 전환 정책 </td> 
   <td colname="col2"> 가능한 경우 재생은 가장 높은 비트 전송률 프로필로 점진적으로 전환됩니다. TVSDK가 프로필 간에 전환하는 속도를 결정하는 ABR 전환에 대한 정책을 설정할 수 있습니다. 기본값은 입니다 <span class="codeph"> MODERATE_POLICY </span>. <p>TVSDK가 더 높은 비트 전송률로 전환하기로 결정하면 플레이어는 현재 ABR 정책에 따라 전환할 이상적인 비트 전송률 프로필을 선택합니다. 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: 대역폭이 현재 비트 전송률보다 50% 높으면 비트 전송률이 다음으로 높은 프로파일로 전환합니다. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: 대역폭이 현재 비트 전송률보다 20% 더 높을 때 다음으로 높은 비트 전송률 프로필로 전환합니다. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGIVE_POLICY </span>: 대역폭이 현재 비트율보다 높을 때 가장 높은 비트율 프로파일로 즉시 전환합니다. </li> 
     </ul> </p> <p>초기 비트 전송률이 0이거나 지정되지 않았지만 정책이 지정된 경우, 재생은 보존에 대한 가장 낮은 비트 전송률 프로필, 보통에 대한 사용 가능한 프로필의 중간 비트 전송률에 가장 가까운 프로필 및 공격성에 대한 가장 높은 비트 전송률 프로필로 시작됩니다. </p> <p>이 속도들이 지정된다면, 이 정책은 최소 및 최대 비트 속도들의 제약들 내에서 작동한다. </p> <p> <span class="codeph"> 정책 </span> 에서 현재 설정을 반환합니다. <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY 또는 AGGRESSIVE_POLICY </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 제어 매개 변수를 엄격히 준수하는 것보다 지속적인 재생 환경을 선호하므로 TVSDK 장애 조치(failover) 메커니즘이 사용자의 설정을 재정의할 수 있습니다.
* 비트 전송률이 변경되면 TVSDK가 발송됩니다. `ProfileEvent.PROFILE_CHANGED`.
* 언제든지 ABR 설정을 변경할 수 있으며 플레이어는 최신 설정과 가장 일치하는 프로필을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있는 경우:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

300000~2000000 범위를 지정하면 TVSDK는 프로필 1, 2 및 3만 고려합니다. 이를 통해 응용 프로그램은 Wi-Fi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 장치로 전환하는 등 다양한 네트워크 조건에 적응할 수 있습니다.

ABR 컨트롤 매개 변수를 설정하려면 다음 중 하나를 수행합니다.

* 사용 `ABRControlParameterBuilder` 매개 변수의 하위 집합을 설정하는 도우미 클래스(다음에서 작동) `ABRControlParameter` 보이지 않는 곳에서)

* 에서 매개 변수 설정 `ABRControlParameter` 클래스.

## ABRControlParametersBuilder를 사용하여 적응형 비트 전송률 구성 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

사용 `ABRControlParametersBuilder` 도우미 클래스는 ABR 매개 변수를 설정하는 가장 간단하고 효율적인 방법입니다.

* 다음 `ABRControlParametersBuilder` 생성자는 모든 ABR 매개 변수를 원본의 기본값으로 설정합니다. `ABRControlParameters` 개체.

* 동일한 ABR에 대한 참조를 유지하는 한 런타임 중에 개별 ABR 매개변수를 재설정할 수 있습니다 `ABRControlParametersBuilder` 인스턴스.

이 클래스에는 `toABRControlParameters()` 도우미 메서드를 사용합니다. 이 메서드를 사용하여 의 인스턴스를 가져옵니다. `ABRControlParameters` 및 설정 `mediaPlayer.ABRControlParameters` 속성. 이렇게 하면 플레이어에서 설정이 적용됩니다.

1. 인스턴스화 `ABRControlParametersBuilder` 도우미 클래스를 참조하고 미디어 플레이어에서 매개 변수를 설정합니다.

   >[!NOTE]
   >
   >예를 들어 다음 샘플은 모든 매개 변수를 기본값으로 초기화한 다음 정책만 보존으로 설정하고 최대 비트 전송률을 1000000으로 제한합니다.
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. 런타임에 개별 ABR 매개 변수를 수정합니다.

   나머지 매개변수는 그대로 두고 개별 매개변수를 수정하려면 다음과 같이 하십시오.

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   이전 설정을 유지하려면 동일한 설정에 대한 참조를 유지해야 합니다 `ABRControlParametersBuilder` 1단계에서 생성한 인스턴스입니다.

## ABRControlParameters를 사용하여 적응형 비트 전송률 구성 {#section_02161FD0A73F40ED9CAE17F9AF850483}

ABR 컨트롤 값은 `ABRControlParameters`, 그러나 언제든지 새 구성을 만들 수 있습니다.

ABR 매개 변수를 설정하는 기능이 `ABRControlParametersBuilder` 클래스이지만 이 기능은 구성 시 ABR 매개변수를 설정하는 데 여전히 효과적입니다. 그러나 구성 후 개별 매개변수를 변경하려면 `ABRControlParametersBuilder` 클래스.

다음 조건은에 적용됩니다. `ABRControlParameters`:

* 구성 시 모든 매개변수에 대한 값을 제공해야 합니다.
* 구성 시간 후에는 개별 값을 변경할 수 없습니다.
* 지정한 매개 변수가 허용 범위를 벗어나는 경우 `ArgumentError` 이 throw됩니다.

1. 초기, 최소 및 최대 비트 전송률을 결정합니다.
1. ABR 정책을 결정합니다.

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 에서 ABR 매개 변수 값을 설정합니다. `ABRControlParameters` 생성자를 지정하고 미디어 플레이어에 할당합니다.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
