---
title: 전역 구성 파일
description: 전역 구성 파일
copied-description: true
exl-id: 109e6e5b-4bb5-43dc-b11e-50799a346a28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 전역 구성 파일{#global-configuration-file}

성능에 가장 큰 영향을 미치는 요소는 전역 구성 파일 flashaccess-global.xml의 설정을 사용하는 것입니다. 이러한 설정에는 다음이 포함됩니다. `<Caching>` 및 `<Logging>` 요소.

* `<Caching>` 다음 `<Caching>` 요소는 메모리에서 구성 파일의 캐싱을 제어합니다. 다음 `<Caching>` element에는 다음 구문이 있습니다.

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 는 서버가 구성 파일에 대한 업데이트를 확인하는 빈도를 제어합니다. 에 대한 낮은 값 `refreshDelaySeconds` 성능은 부정적인 영향을 받는 반면, 값이 높을수록 성능이 향상될 수 있습니다. 에 대한 자세한 내용 `refreshDelaySeconds`, 참조 &quot;[구성 파일 업데이트 중](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` 테넌트의 수를 지정합니다. 테넌트 수보다 낮은 값은 나머지 테넌트에 대한 요청으로 인해 캐시 누락이 발생하므로 성능에 영향을 줄 수 있습니다. 구성 데이터에 대한 캐시 누락은 성능에 부정적인 영향을 줍니다. 따라서 Adobe은 고려해야 할 메모리 제한이 없는 한 이 값을 서버에 구성된 테넌트 수보다 높게 설정할 것을 권장합니다.

* `<Logging>` 다음 `<Logging>` element는 로깅 수준과 로그 파일이 롤링되는 빈도를 지정합니다. 다음 `<Logging>` element에는 다음 구문이 있습니다.

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 기록할 메시지를 지정합니다. 값이 &quot;DEBUG&quot;이면 로그 메시지가 많이 생성되므로 성능에 부정적인 영향을 줄 수 있습니다. Adobe은 최적의 성능을 위해 &quot;경고&quot; 설정을 권장합니다. 그러나 이 값은 라이센스 감사와 같은 필수 런타임 정보를 손실할 위험이 있습니다. 성능에 미치는 영향을 최소화하면서 중요한 로그 정보를 보존하려면 &quot;INFO&quot; 값을 사용하십시오.
   * `rollingFrequency` 로그 파일의 빈도를 지정합니다 *롤링됨*. 롤링은 이전 활성 로그 파일이 더 이상 기록되지 않고 롤링으로 간주되는 동안 새 로그 파일이 활성 로그가 되는 프로세스입니다. 롤링 간격은 &quot;MINUTES&quot;, &quot;HOURLY&quot;, &quot;TWO-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; 또는 &quot;NEVER&quot;로 설정할 수 있습니다.

다음을 참조하십시오 *컨텐츠 보호를 위해 Adobe 액세스 SDK 사용* 성능 최적화에 대한 추가 팁입니다.
