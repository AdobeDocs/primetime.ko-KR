---
description: 이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 설정은 성능에 영향을 줍니다.
title: 전역 구성 파일
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 성능 조정 {#performance-tuning}

이 항목에서는 성능 관련 고려 사항에 대해 설명합니다. flashaccess-global.xml이라는 전역 구성 파일의 설정은 성능에 영향을 줍니다.

## 전역 구성 파일 {#global-configuration-file}

구성 파일에는 다음 설정 요소가 포함되어 있습니다.

* `<Caching>` 다음 `<Caching>` 요소는 메모리에서 구성 파일의 캐싱을 제어합니다. 다음 `<Caching>` 요소는 다음 구문을 지원합니다.

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 서버가 구성 파일에 대한 업데이트를 확인하는 빈도를 제어합니다. 에 대한 낮은 값 `refreshDelaySeconds` 성능에 부정적인 영향을 주지만 값이 높을수록 성능이 향상될 수 있습니다.

  다음을 참조하십시오 *구성 파일 업데이트 중* 에 대한 추가 정보를 위해 `refreshDelaySeconds`.

* `numTenants` 테넌트의 수를 지정합니다. 테넌트 수보다 낮은 값은 나머지 테넌트에 대한 요청으로 인해 캐시 누락이 발생하므로 성능에 영향을 줍니다. 구성 데이터의 캐시 누락으로 인해 성능에 부정적인 영향을 미칩니다. 따라서 고려해야 하는 메모리 제한이 없는 한 이 값을 서버에 대해 구성된 테넌트 수보다 높게 설정하는 것이 좋습니다.

* `<Logging>` 다음 `<Logging>` element는 로그 파일이 롤링되는 빈도와 로깅 수준을 지정합니다. 다음 `<Logging>` 요소는 다음 구문을 지원합니다.

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` 로그에 대한 메시지를 지정합니다. 값 `DEBUG` 은 많은 로그 메시지를 생성하므로 성능에 부정적인 영향을 줄 수 있습니다. 다음의 설정을 적용하는 것이 좋습니다. `WARN` 최적의 성능을 위해 그러나 이 값을 사용하면 라이센스 감사와 같은 필수 런타임 정보가 손실될 수 있습니다. 성능에 미치는 영향을 최소화하면서 로그 정보를 저장하려면 다음 값을 적용해야 합니다. `INFO`.

* `<rollingFrequency>`  `rollingFrequency` 로그 파일의 빈도를 지정합니다 *롤링됨*. *`Rolling`* 는 새 로그 파일을 활성 로그로 지정하는 프로세스입니다. 따라서 이전의 활성 로그 파일은 더 이상 수정할 수 없으며 로 간주됩니다 *`rolled`*. 롤링 간격을 다음으로 설정할 수 있습니다. `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`, 또는 `NEVER`.

다음을 참조하십시오 *컨텐츠 보호를 위해 Adobe Primetime DRM SDK 사용* 성능을 최적화하는 방법에 대한 팁입니다.
