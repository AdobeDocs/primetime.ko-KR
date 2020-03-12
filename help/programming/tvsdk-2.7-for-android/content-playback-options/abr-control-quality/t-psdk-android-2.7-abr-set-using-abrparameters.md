---
description: ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.
seo-description: ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.
seo-title: ABRControlParameters를 사용하여 적응형 비트 전송률 구성
title: ABRControlParameters를 사용하여 적응형 비트 전송률 구성
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# ABRControlParameters를 사용하여 적응형 비트 전송률 구성 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

ABR 컨트롤 값은 ABRControlParameters에서만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.

다음 조건이 `ABRControlParameters`적용됩니다.

* 구성 시 모든 매개 변수에 대한 값을 제공해야 합니다.
* 구성 후에는 개별 값을 변경할 수 없습니다.
* 지정한 매개 변수가 허용된 범위를 벗어나는 경우 `ArgumentError` 가 발생합니다.

1. 초기, 최소 및 최대 비트 속도를 결정할 수 있습니다.
1. ABR 정책 결정:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 생성자에서 ABR 매개 변수 값을 `ABRControlParameters` 설정하고 이 값을 Media Player에 할당합니다.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```

