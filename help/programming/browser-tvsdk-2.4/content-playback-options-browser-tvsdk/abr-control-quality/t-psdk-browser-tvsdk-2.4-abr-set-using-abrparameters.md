---
description: ABR 컨트롤 값은 ABRControlParameters로만 설정할 수 있지만 언제든지 새 값을 구성할 수 있습니다.
title: ABRControlParameters를 사용하여 적응형 비트 전송률 구성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# ABRControlParameters를 사용하여 적응형 비트 전송률 구성{#configure-adaptive-bit-rates-using-abrcontrolparameters}

ABR 컨트롤 값은 ABRControlParameters로만 설정할 수 있지만 언제든지 새 값을 구성할 수 있습니다.

다음 조건은에 적용됩니다. `ABRControlParameters`:

* 구성 시 모든 매개변수에 대한 값을 제공해야 합니다.
* 구성 시간 후에는 개별 값을 변경할 수 없습니다.
* 지정한 매개 변수가 허용 범위를 벗어나는 경우 `ArgumentError` 이 throw됩니다.

1. ABR 정책을 결정합니다.

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 에서 ABR 매개 변수 값을 설정합니다. `ABRControlParameters` 생성자를 지정하고 미디어 플레이어에 할당합니다.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
