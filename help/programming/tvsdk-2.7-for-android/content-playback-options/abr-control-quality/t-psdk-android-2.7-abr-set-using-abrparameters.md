---
description: ABR 컨트롤 값은 ABRControlParameters로만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.
title: ABRControlParameters를 사용하여 응용 비트 전송률 구성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}를 사용하여 응용 비트 전송률 구성

ABR 컨트롤 값은 ABRControlParameters로만 설정할 수 있지만 언제든지 새 컨트롤을 만들 수 있습니다.

다음 조건이 `ABRControlParameters`에 적용됩니다.

* 구성 시에는 모든 매개 변수에 대한 값을 제공해야 합니다.
* 구성 후에는 개별 값을 변경할 수 없습니다.
* 지정한 매개 변수가 허용된 범위를 벗어나는 경우 `ArgumentError`이(가) 발생합니다.

1. 초기, 최소 및 최대 비트 속도를 결정합니다.
1. ABR 정책 결정:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. `ABRControlParameters` 생성자에서 ABR 매개 변수 값을 설정하고 이 값을 미디어 플레이어에 할당합니다.

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

