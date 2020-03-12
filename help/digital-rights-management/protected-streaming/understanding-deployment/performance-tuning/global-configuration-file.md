---
description: 이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 모든 설정은 성능에 영향을 줍니다.
seo-description: 이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 모든 설정은 성능에 영향을 줍니다.
seo-title: 전역 구성 파일
title: 전역 구성 파일
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 성능 조정 {#performance-tuning}

이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 모든 설정은 성능에 영향을 줍니다.

## 전역 구성 파일 {#global-configuration-file}

구성 파일에는 다음 설정 요소가 포함됩니다.

* `<Caching>` 이 `<Caching>` 요소는 메모리에 있는 구성 파일의 캐싱을 제어합니다. 이 `<Caching>` 요소는 다음 구문을 지원합니다.

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 서버가 구성 파일에 대한 업데이트를 확인하는 빈도를 제어합니다. 낮은 값을 지정하면 성능이 저하되고 `refreshDelaySeconds` 높은 값을 지정하면 성능이 향상될 수 있습니다.

   자세한 *내용은 구성 파일* 업데이트를 참조하십시오 `refreshDelaySeconds`.

* `numTenants` 테넌트 수를 지정합니다. 테넌트 수보다 낮은 값은 나머지 테넌트에 대한 요청으로 인해 캐시 오류가 발생하기 때문에 성능에 영향을 줍니다. 모든 구성 데이터의 캐시 누락은 성능에 부정적인 영향을 줍니다. 따라서 고려해야 하는 메모리 제한이 없는 경우 서버에 대해 구성된 테넌트 수보다 높게 이 값을 설정하는 것이 좋습니다.

* `<Logging>` 이 `<Logging>` 요소는 로그 파일이 롤링되는 빈도 및 로깅 수준을 지정합니다. 이 `<Logging>` 요소는 다음 구문을 지원합니다.

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  로그에 메시지를 `level` 지정합니다. 의 값은 많은 로그 메시지를 `DEBUG` 생성하므로 성능에 부정적인 영향을 줄 수 있습니다. 최적의 성능을 `WARN` 위해 설정을 적용하는 것이 좋습니다. 그러나 이 값은 라이센스 감사와 같은 필수 런타임 정보를 잃게 됩니다. 성능에 미치는 영향을 최소화하면서 로그 정보를 저장하려면 의 값을 적용해야 합니다 `INFO`.

* `<rollingFrequency>`  로그 `rollingFrequency` 파일의 *롤링*&#x200B;빈도를 지정합니다. *`Rolling`* 는 새 로그 파일을 활성 로그로 지정하는 프로세스입니다. 따라서 이전에 활성 상태였던 로그 파일은 더 이상 수정할 수 없으며, 수정되는 것으로 간주됩니다 *`rolled`*. 롤링 간격을 `MINUTELY`, `HOURLY`, `TWICE-DAILY``DAILY`, `WEEKLY``MONTHLY`, `NEVER`또는로 설정할 수있습니다.

성능을 *최적화하는 방법에 대한 팁은 Adobe Primetime DRM* SDK를 사용하여 콘텐츠 보호를 참조하십시오.