---
seo-title: 전역 구성 파일
title: 전역 구성 파일
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 전역 구성 파일{#global-configuration-file}

성능에 가장 큰 영향을 미치는 것은 전역 구성 파일의 flashaccess-global.xml 설정을 사용하는 것입니다. 이러한 설정에는 `<Caching>` 및 `<Logging>` 요소가 포함됩니다.

* `<Caching>` 이 `<Caching>` 요소는 메모리에 있는 구성 파일의 캐싱을 제어합니다. 이 `<Caching>` 요소에는 다음 구문이 있습니다.

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 서버가 구성 파일에 대한 업데이트를 확인하는 빈도를 제어합니다. 낮은 값은 성능에 `refreshDelaySeconds` 부정적인 영향을 주는 반면, 높은 값은 성능을 향상시킬 수 있습니다. 자세한 내용은 `refreshDelaySeconds`&quot;구성 파일[업데이트](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;를 참조하십시오.

   * `numTenants` 테넌트 수를 지정합니다. 테넌트 수보다 낮은 값은 나머지 세입자에 대한 요청이 캐시 실패를 야기하기 때문에 성능에 영향을 줍니다. 구성 데이터에 대한 캐시 누락은 성능에 부정적인 영향을 줍니다. 따라서 고려해야 할 메모리 제한이 없는 한 이 값을 서버에 대해 구성된 테넌트 수보다 높게 설정하는 것이 좋습니다.

* `<Logging>` 이 `<Logging>` 요소는 로깅 수준 및 로그 파일의 롤링 빈도를 지정합니다. 이 `<Logging>` 요소에는 다음 구문이 있습니다.

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 기록할 메시지를 지정합니다. &quot;DEBUG&quot; 값은 로그 메시지가 많이 생성되며 성능에 부정적인 영향을 줄 수 있습니다. 최적의 성능을 위해 &quot;WARN&quot; 설정을 사용하는 것이 좋습니다. 그러나 이러한 가치는 라이센스 감사와 같은 필수적인 런타임 정보를 잃을 위험이 있습니다. 성능에 영향을 미치지 않으면서 중요한 로그 정보를 보존하려면 &quot;INFO&quot; 값을 사용하십시오.
   * `rollingFrequency` 로그 파일의 *롤링*&#x200B;빈도를 지정합니다. 롤링은 새 로그 파일이 활성 로그가 되는 프로세스이며, 이전에 활성 로그 파일은 더 이상 기록되지 않고 롤링된 것으로 간주됩니다. 롤링 간격은 &quot;MINITERLY&quot;, &quot;HOURLY&quot;, &quot;TWENTLY-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; 또는 &quot;NEVER&quot;로 설정할 수 있습니다.

성능 최적화에 *대한 추가 팁은 콘텐츠 보호를* 위한 Adobe Access SDK 사용을 참조하십시오.
