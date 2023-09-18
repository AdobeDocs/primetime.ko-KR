---
title: 성능 조정
description: 성능 조정
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 성능 조정{#performance-tuning}

다음 팁을 사용하여 성능을 높이십시오.

* 네트워크 HSM을 사용하는 것은 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있다.
* 성능을 개선하기 위해 의 플랫폼별 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 활성화할 수도 있습니다. [!DNL thirdparty/cryptoj] SDK 폴더. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가합니다.

  >[!NOTE]
  >
  >동일한 Tomcat 인스턴스에서 여러 웹 응용 프로그램을 실행하고 `jsafe.dll` 경로에서 로드되는 첫 번째 웹 애플리케이션만 `jsafe.dll` 라이브러리입니다. 따라서 첫 번째 웹 애플리케이션만 기본 지원의 이점을 얻을 수 있습니다. 이러한 경우 모든 웹 애플리케이션의 성능을 향상시키려면 다음을 수행하십시오. `cryptoj.jar`WAR 파일 외부. 예를 들어, `<tomcat_installation_folder>/lib` 디렉토리.

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 뛰어난 성능을 제공합니다.

## 난수 생성(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

특정 조건에서 Linux 환경은 다음을 포함하여 난수 생성이 필요한 Primetime DRM 관련 작업을 수행할 때 일시 중지할 수 있습니다.

* Adobe Primetime DRM 라이센스 서버 시작
* 을(를) 사용한 정책 생성 [!DNL AdobePolicyManager] 유틸리티
* Adobe Media Server 또는 Primetime OfflinePackager로 DRM 보호 콘텐츠 패키징

이러한 작업 중 지연은 Linux 서버의 낮은 엔트로피 풀의 결과인 경우가 많습니다.

Linux에서는 서버 환경의 엔트로피 풀에서 난수가 생성됩니다. 엔트로피 풀은 일반적으로 리눅스 커널에 의해 하드웨어 인터럽트를 수신함으로써 유지된다. 서버가 격리되어 있고 HW 리소스(예: 마우스 또는 키보드)로부터 정기적인 입력을 수신하지 않는 경우, 엔트로피 풀을 리필하기 위한 대기가 연장될 수 있다. 이 시나리오에서는 의 데이터를 기다리는 작업이 [!DNL /dev/random] 일시 정지 가능.

Linux 서버에서 하드웨어 난수 생성기를 사용하여 충분한 엔트로피가 생성되도록 할 수 있습니다. 그러나 주어진 배포 시나리오에서 하드웨어 난수 생성기를 사용할 수 없는 경우 소프트웨어 기반 솔루션을 사용하여 엔트로피 풀 새로 고침 빈도를 높일 수 있습니다. Linux에서 이러한 소프트웨어 솔루션 중 하나는 [!DNL haveged] (HArdware 휘발성 엔트로피 수집 및 확장 데몬).

## 사용 가능한 엔트로피 결정 {#section_686B311FE6144566B6939E9F20915ADC}

예기치 않은 지연 동안 주어진 서버의 엔트로피 풀에서 사용할 수 있는 비트 수를 확인하려면 다음 명령을 실행합니다.

```
cat /proc/sys/kernel/random/entropy_avail 
```

많은 엔트로피를 사용할 수 있는 건강한 리눅스 시스템은 4,096비트의 전체 엔트로피를 반환할 것이다. 반환된 값이 200보다 작으면 계는 엔트로피가 매우 낮게 작동한다.
