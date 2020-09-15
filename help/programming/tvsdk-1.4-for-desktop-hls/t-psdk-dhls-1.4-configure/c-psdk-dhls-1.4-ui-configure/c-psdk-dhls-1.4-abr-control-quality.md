---
description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-description: HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.
seo-title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
title: 비디오 품질을 위한 ABR(적응형 비트 전송률)
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---


# 비디오 품질을 위한 ABR(적응형 비트 전송률){#adaptive-bit-rates-abr-for-video-quality}

HLS 및 DASH 스트림은 동일한 짧은 비디오 버스트에 대해 서로 다른 비트 전송률 인코딩(프로필)을 제공합니다. TVSDK는 사용 가능한 대역폭에 따라 각 버스트에 대한 품질 수준을 선택할 수 있습니다.

TVSDK는 컨텐츠가 현재 네트워크 연결에 대해 최적의 비트 전송률로 재생되도록 항상 비트 전송률을 모니터링합니다.

ABR(응용 비트 전송률) 전환 정책과 MBR(다중 비트 전송률) 스트림에 대한 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성에서 최적의 재생 경험을 제공하는 비트 전송률로 자동 전환됩니다.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> 초기 비트 전송률 </td> 
   <td colname="col2"> <p>첫 번째 세그먼트에 대한 원하는 재생 비트 속도(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 가장 가까운 프로파일인 초기 비트 전송률보다 크거나 같습니다. </p> <p> 최소 비트 전송률을 정의하고 초기 비트 전송률이 최소 비트율보다 낮은 경우 TVSDK는 최소 비트 전송률보다 낮은 비트 전송률을 갖는 프로파일을 선택합니다. 초기 비율이 최대 속도보다 높은 경우 TVSDK는 최대 속도보다 가장 높은 비율을 선택합니다. </p> <p>초기 비트 전송률이 0이거나 정의되지 않은 경우 초기 비트 전송률은 ABR 정책에 의해 결정됩니다. </p> <p> <span class="apiname"> ABRI초기BitRate </span> 는 초당 바이트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최소 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 허용되는 가장 낮은 비트 전송률입니다. ABR 전환은 비트 전송률이 이 비트율보다 낮은 프로필을 무시합니다. </p> <p> <span class="apiname"> ABRMinBitRate </span> 는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> 최대 비트 전송률 </td> 
   <td colname="col2"> <p>ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR 전환은 비트율보다 비트 속도가 높은 프로파일을 무시합니다. </p> <p> <span class="apiname"> ABRMaxBitRate </span> 는 초당 비트 프로필을 나타내는 정수 값을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR 전환 정책 </td> 
   <td colname="col2"> 재생은 가능한 경우 가장 높은 비트 전송률 프로파일로 점차 전환됩니다. ABR 전환을 위한 정책을 설정할 수 있습니다. 이 정책은 TVSDK가 프로필 간에 전환되는 속도를 결정합니다. 기본값은 <span class="codeph"> MODERATE_POLICY입니다 </span>. <p>TVSDK가 더 높은 비트 전송률을 전환할 경우 플레이어는 현재 ABR 정책을 기반으로 전환하기 위한 이상적인 비트 전송률 프로필을 선택합니다. 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> RELATIVE_POLICY </span>:대역폭이 현재 비트 전송률보다 50% 높을 때 비트 전송률이 다음으로 높은 프로필로 전환합니다. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>:대역폭이 현재 비트 전송률보다 20% 높을 때 다음 높은 비트 전송률 프로파일로 전환합니다. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> 공격적인 정책 </span>:대역폭이 현재 비트 전송률보다 높은 경우 즉시 가장 높은 비트 전송률 프로파일로 전환됩니다. </li> 
     </ul> </p> <p>초기 비트 전송률이 0이거나 지정되지 않았지만 정책을 지정한 경우 재생은 고품질의 가장 낮은 비트 전송률 프로필, 중간값을 위해 사용 가능한 프로필의 중간값 비트 전송률에 가장 가까운 프로필, 공격성을 위해 가장 높은 비트 전송률 프로필로 시작합니다. </p> <p>이러한 속도가 지정된 경우 정책은 최소 및 최대 비트 전송률의 제한에서 작동합니다. </p> <p> <span class="codeph"> ABRPolicy </span> 는 ABRControlParameters <span class="codeph"> 열거에서 현재 설정을 </span> 반환합니다.REVENTOR_POLICY, MODERATE_POLICY 또는 AGAINST_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

다음 정보를 염두에 두십시오.

* TVSDK는 제어 매개 변수를 엄격히 준수하면서 지속적인 재생 환경을 선호하므로 TVSDK 페일오버 메커니즘이 사용자 설정을 무시할 수 있습니다.
* 비트 전송률이 변경되면 TVSDK가 전달합니다 `ProfileEvent.PROFILE_CHANGED`.
* 언제든지 ABR 설정을 변경할 수 있으며, 플레이어는 가장 최근 설정과 가장 유사한 프로파일을 사용하도록 전환합니다.

예를 들어 스트림에 다음 프로필이 있을 경우:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

300000 ~ 200000의 범위를 지정하는 경우 TVSDK는 프로파일 1, 2 및 3만 고려합니다. 이를 통해 애플리케이션은 wi-fi에서 3G로 전환하거나 휴대폰, 태블릿 또는 데스크탑 컴퓨터와 같은 다양한 디바이스로 전환하는 등 다양한 네트워크 조건에 맞게 조정할 수 있습니다.

ABR 제어 매개 변수를 설정하려면 다음 중 하나를 수행합니다.

* 도우미 `ABRControlParameterBuilder` 클래스를 사용하여 매개 변수의 하위 집합을 설정합니다(백그라운드 `ABRControlParameter` 에서 작동).

* 클래스에 매개 변수를 `ABRControlParameter` 설정합니다.

## ABRControlParametersBuilder를 사용하여 응용 비트 전송률 구성 {#section_3DDE397A7CE445E1832EBAA46CE5C069}

ABR 매개 변수를 설정하는 가장 간단하고 효율적인 방법은 `ABRControlParametersBuilder` 도우미 클래스를 사용하는 것입니다.

* 생성자는 모든 ABR 매개 변수를 기본 개체에 대한 기본값으로 `ABRControlParametersBuilder` `ABRControlParameters` 설정합니다.

* 동일한 인스턴스에 대한 참조를 유지하는 한 런타임 동안 개별 ABR 매개 변수를 재설정할 수 `ABRControlParametersBuilder` 있습니다.

이 클래스에는 `toABRControlParameters()` 도우미 메서드도 포함되어 있습니다. 이 메서드를 사용하여 인스턴스 `ABRControlParameters` 를 가져와 속성에 `mediaPlayer.ABRControlParameters` 설정합니다. 그러면 플레이어에서 설정이 적용됩니다.

1. 도우미 클래스를 `ABRControlParametersBuilder` 인스턴스화하고 Media Player에서 매개 변수를 설정합니다.

   >[!NOTE]
   >
   >예를 들어 다음 샘플에서는 모든 매개 변수를 기본값으로 초기화한 다음, 정책만 보수적으로 설정하고 최대 비트 전송률을 100000으로 제한합니다.
   >
   >
   ```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```

1. 런타임에 개별 ABR 매개 변수를 수정합니다.

   나머지 매개 변수를 그대로 유지하면서 개별 매개 변수를 수정하려면 다음을 수행하십시오.

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   이전 설정을 유지하려면 1단계에서 만든 동일한 인스턴스에 대한 참조를 `ABRControlParametersBuilder` 유지해야 합니다.

## ABRConcontrolParameters를 사용하여 응용 비트 전송률 구성 {#section_02161FD0A73F40ED9CAE17F9AF850483}

ABR 컨트롤 값은 를 통해서만 설정할 수 `ABRControlParameters`있지만 언제든지 새 값을 만들 수 있습니다.

ABR 매개 변수를 설정하는 기능은 클래스가 존재하기 전에 지원되었지만 이 기능은 `ABRControlParametersBuilder` 구성 시 ABR 매개 변수를 설정하는 데 여전히 효과적입니다. 그러나 구성 후 개별 매개 변수를 변경하려면 `ABRControlParametersBuilder` 클래스를 사용해야 합니다.

다음 조건이 적용됩니다 `ABRControlParameters`.

* 구성 시 모든 매개변수에 대한 값을 제공해야 합니다.
* 구성 시간 후에는 개별 값을 변경할 수 없습니다.
* 지정하는 매개 변수가 허용된 범위를 벗어나는 경우 `ArgumentError` 가 throw됩니다.

1. 초기, 최소 및 최대 비트 전송률을 결정할 수 있습니다.
1. ABR 정책 결정:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. 생성자에서 ABR 매개 변수 값을 `ABRControlParameters` 설정하고 Media Player에 할당합니다.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

