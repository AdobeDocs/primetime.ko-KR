---
description: ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.
seo-description: ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.
seo-title: ABRControlParameters를 사용하여 적응형 비트 전송률 구성
title: ABRControlParameters를 사용하여 적응형 비트 전송률 구성
uuid: 99b7a463-327b-48bf-8244-e41467072b44
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# ABRControlParameters를 사용하여 적응형 비트 전송률 구성{#configure-adaptive-bit-rates-using-abrcontrolparameters}

ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.

다음 조건이 `ABRControlParameters`적용됩니다.

* 구성 시 모든 매개 변수에 대한 값을 제공해야 합니다.
* 구성 시간 후에는 개별 값을 변경할 수 없습니다.
* 지정한 매개 변수가 허용된 범위를 벗어나는 경우 `ArgumentError` 가 발생합니다.

1. ABR 정책 결정:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 생성자에서 ABR 매개 변수 값을 `ABRControlParameters` 설정하고 Media Player에 할당합니다.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

