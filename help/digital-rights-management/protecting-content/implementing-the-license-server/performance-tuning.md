---
title: 성능 조정
description: 성능 조정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 성능 조정{#performance-tuning}

성능을 높이려면 다음 팁을 사용합니다.

* 네트워크 HSM 사용 속도는 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있습니다.
* 성능을 향상시키려면 SDK의 [!DNL thirdparty/cryptoj] 폴더에 있는 플랫폼 특정 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 선택적으로 활성화할 수 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가하십시오.

   >[!NOTE]
   >
   >동일한 Tomcat 인스턴스에서 여러 웹 애플리케이션을 실행하고 경로에 `jsafe.dll`이 있는 경우 로드되는 첫 번째 웹 애플리케이션만 `jsafe.dll` 라이브러리를 로드할 수 있습니다. 따라서 기본 지원을 통해 첫 번째 웹 애플리케이션만 혜택을 받을 수 있습니다. 이러한 경우 모든 웹 응용 프로그램의 성능을 향상하려면 WAR 파일 외부에 `cryptoj.jar`을(를) 배치합니다. 예를 들어 `<tomcat_installation_folder>/lib` 디렉토리에 있습니다.

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제에 비해 훨씬 향상된 성능을 제공합니다.

## 난수 생성(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

특정 조건에서 Linux 환경은 무작위 번호 생성이 필요한 Primetime DRM 관련 작업을 수행할 때 다음을 비롯하여 일시 중지할 수 있습니다.

* Adobe Primetime DRM 라이선스 서버 시작
* [!DNL AdobePolicyManager] 유틸리티를 사용한 정책 생성
* Adobe Medium 서버 또는 Primetime OfflinePackager를 사용하여 DRM으로 보호된 콘텐츠 패키징

이러한 작업 중 지연은 종종 Linux 서버에 낮은 엔트로피 풀이 발생하는 경우가 많습니다.

Linux의 경우 서버 환경의 엔트로피 풀에서 무작위 숫자가 생성됩니다. 엔트로피 풀은 일반적으로 Linux 커널로 하드웨어 인터럽트를 수신하여 유지 관리됩니다. 서버가 격리되어 있고 HW 리소스(예: 마우스 또는 키보드)로부터 일반적인 입력을 받지 못하는 경우 엔트로피 풀을 다시 채울 때까지 대기할 수 있습니다. 이 시나리오에서는 [!DNL /dev/random]의 데이터를 기다리는 작업이 일시 중지될 수 있습니다.

충분한 엔트로피가 생성되도록 Linux 서버에서 하드웨어 무작위 번호 생성기를 사용할 수 있습니다. 그러나 주어진 배포 시나리오에서 하드웨어 무작위 번호 생성기를 사용할 수 없는 경우 소프트웨어 기반 솔루션을 사용하여 엔트로피 풀 새로 고침 속도를 늘릴 수 있습니다. Linux에서 이러한 소프트웨어 솔루션 중 하나가 [!DNL haveged](HArdware 휘발성 엔트로피 수집 및 확장 데몬)입니다.

## 사용 가능한 엔트로피 확인 중 {#section_686B311FE6144566B6939E9F20915ADC}

예기치 않은 지연 중에 지정된 서버의 엔트로피 풀에서 사용할 수 있는 비트 수를 확인하려면 다음 명령을 실행하십시오.

```
cat /proc/sys/kernel/random/entropy_avail 
```

많은 엔트로피가 있는 건강한 리눅스 시스템은 4,096비트의 엔트로피의 완전한 상태를 되찾을 것이다. 반환된 값이 200보다 작으면 시스템은 엔트로피의 매우 낮은 상태를 유지합니다.
