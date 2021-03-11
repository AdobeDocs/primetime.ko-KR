---
description: 이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 모든 설정은 성능에 영향을 줍니다.
title: 전역 구성 파일
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 성능 조정 {#performance-tuning}

이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 모든 설정은 성능에 영향을 줍니다.

## 전역 구성 파일 {#global-configuration-file}

구성 파일에는 다음 설정 요소가 포함됩니다.

* `<Caching>` 이  `<Caching>` 요소는 메모리에 구성 파일의 캐시를 제어합니다. `<Caching>` 요소는 다음 구문을 지원합니다.

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 서버가 구성 파일의 업데이트를 확인하는 빈도를 제어합니다. `refreshDelaySeconds`의 값이 낮으면 성능에 부정적인 영향을 주고, 값이 높으면 성능이 향상될 수 있습니다.

   `refreshDelaySeconds`에 대한 자세한 내용은 *구성 파일 업데이트*&#x200B;를 참조하십시오.

* `numTenants` 세입자 수를 지정합니다. 세입자 수보다 작은 값은 나머지 세입자에 대한 요청은 캐시 누락으로 이어지기 때문에 성능에 영향을 줍니다. 모든 구성 데이터에 대한 캐시가 성능에 부정적인 영향을 줍니다. 따라서 고려해야 하는 메모리 제한이 없는 한 서버에 대해 구성된 테넌트 수보다 높은 값을 설정하는 것이 좋습니다.

* `<Logging>` 이  `<Logging>` 요소는 로그 파일을 롤링하는 로깅 수준과 빈도를 지정합니다. `<Logging>` 요소는 다음 구문을 지원합니다.

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 로그에 메시지를 지정합니다. `DEBUG` 값을 사용하면 로그 메시지가 많이 생성되므로 성능에 부정적인 영향을 줄 수 있습니다. 최적의 성능을 위해 `WARN` 설정을 적용하는 것이 좋습니다. 그러나 이 값을 통해 라이센스 감사와 같은 중요한 런타임 정보가 손실될 수 있습니다. 성능에 미치는 영향을 최소화하면서 로그 정보를 저장하려면 `INFO` 값을 적용해야 합니다.

* `<rollingFrequency>`  `rollingFrequency` 로그 파일의  *롤링* 빈도를 지정합니다. *`Rolling`* 는 새 로그 파일을 활성 로그로 지정하는 프로세스입니다. 따라서 이전에 활성 상태였던 로그 파일은 더 이상 수정할 수 없으며 *`rolled`*&#x200B;으로 간주됩니다. 롤링 간격을 `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` 또는 `NEVER`로 설정할 수 있습니다.

성능을 최적화하는 방법에 대한 팁은 *콘텐츠 보호를 위한 Adobe Primetime DRM SDK 사용을 참조하십시오.*