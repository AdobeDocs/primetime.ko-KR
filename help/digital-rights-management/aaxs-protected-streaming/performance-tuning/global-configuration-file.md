---
title: 전역 구성 파일
description: 전역 구성 파일
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# 전역 구성 파일{#global-configuration-file}

성능에 가장 큰 영향을 미치는 것은 전역 구성 파일인 flashaccess-global.xml의 설정을 사용하는 것입니다. 이러한 설정에는 `<Caching>` 및 `<Logging>` 요소가 포함됩니다.

* `<Caching>` 이  `<Caching>` 요소는 메모리에 구성 파일의 캐시를 제어합니다. `<Caching>` 요소에는 다음 구문이 있습니다.

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 서버가 구성 파일에 대한 업데이트를 확인하는 빈도를 제어합니다. `refreshDelaySeconds`의 낮은 값은 성능에 부정적인 영향을 주고, 높은 값은 성능을 향상시킬 수 있습니다. `refreshDelaySeconds`에 대한 자세한 내용은 &quot;[구성 파일 업데이트](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;를 참조하십시오.

   * `numTenants` 세입자 수를 지정합니다. 세입자 수보다 낮은 값은 나머지 세입자에 대한 요청으로 인해 캐시 누락이 발생하므로 성능에 영향을 줍니다. 구성 데이터의 캐시가 성능에 부정적인 영향을 줍니다. 따라서 고려해야 할 메모리 제한이 없는 경우 Adobe은 서버에 대해 구성된 테넌트 수보다 높은 값을 설정할 것을 권장합니다.

* `<Logging>` 이  `<Logging>` 요소는 로깅 수준과 로그 파일의 롤링 빈도를 지정합니다. `<Logging>` 요소에는 다음 구문이 있습니다.

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 기록할 메시지를 지정합니다. &quot;DEBUG&quot; 값은 로그 메시지가 많이 생성되며 성능에 부정적인 영향을 줄 수 있습니다. Adobe에서는 최적의 성능을 위해 &quot;WARN&quot; 설정을 권장합니다. 그러나 이러한 가치는 라이센스 감사와 같은 중요한 런타임 정보를 잃게 될 위험이 있습니다. 성능에 미치는 영향을 최소화하면서 중요한 로그 정보를 보존하려면 &quot;INFO&quot; 값을 사용하십시오.
   * `rollingFrequency` 로그 파일의  *롤링* 빈도를 지정합니다. 롤링은 새 로그 파일이 활성 로그가 되는 프로세스이며, 이전에 활성 로그 파일은 더 이상 기록되지 않고 롤링되는 것으로 간주됩니다. 롤링 간격은 &quot;MINITERLY&quot;, &quot;HOURLY&quot;, &quot;TWIST-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; 또는 &quot;NEVER&quot;로 설정할 수 있습니다.

성능 최적화에 대한 추가 팁은 *콘텐츠 보호를 위한 Adobe 액세스 SDK 사용을 참조하십시오*.
