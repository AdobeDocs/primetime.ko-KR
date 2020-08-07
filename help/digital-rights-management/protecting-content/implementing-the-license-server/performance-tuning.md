---
seo-title: 성능 조정
title: 성능 조정
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 성능 조정{#performance-tuning}

다음 팁을 사용하여 성능을 높이십시오.

* 네트워크 HSM을 사용하는 것은 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있습니다.
* 성능 향상을 위해 SDK의 폴더에 있는 플랫폼 특정 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 선택적으로 활성화할 수 [!DNL thirdparty/cryptoj] 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가하십시오.

   >[!NOTE]
   >
   >동일한 Tomcat 인스턴스에서 여러 웹 애플리케이션을 실행하고 경로에 있는 경우 `jsafe.dll` 는 첫 번째 웹 애플리케이션만 `jsafe.dll` 라이브러리를 로드할 수 있습니다. 따라서 기본 지원을 통해 첫 번째 웹 애플리케이션만 혜택을 받을 수 있습니다. 이러한 경우 모든 웹 애플리케이션의 성능을 향상시키려면 WAR 파일 `cryptoj.jar`외부에 추가하십시오. 예: in the directory. `<tomcat_installation_folder>/lib`

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제에서 훨씬 향상된 성능을 제공합니다.

## 난수 생성(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

특정 조건에서 Linux 환경은 다음과 같은 무작위 숫자 생성이 필요한 Primetime DRM 관련 작업을 수행할 때 일시 중지할 수 있습니다.

* Adobe Primetime DRM 라이선스 서버 시작
* 유틸리티를 사용한 정책 [!DNL AdobePolicyManager] 생성
* Adobe 미디어 서버 또는 Primetime OfflinePackager를 사용하여 DRM으로 보호된 콘텐츠 패키징

이러한 작업 중 지연은 종종 Linux 서버의 낮은 엔트로피 풀의 결과입니다.

Linux의 경우 서버 환경의 엔트로피 풀에서 무작위 숫자가 생성됩니다. 엔트로피 풀은 일반적으로 Linux 커널로 하드웨어 인터럽트를 수신하여 유지 관리됩니다. 서버가 격리되어 있고 HW 리소스(예: 마우스 또는 키보드)로부터 정기적인 입력을 받지 못하는 경우 엔트로피 풀을 다시 채울 때까지 대기할 수 있습니다. 이 시나리오에서 데이터를 기다리는 작업이 일시 중지될 수 [!DNL /dev/random] 있습니다.

Linux 서버에서 하드웨어 무작위 번호 생성기를 사용하여 충분한 엔트로피가 생성되도록 할 수 있습니다. 그러나 주어진 배포 시나리오에서 하드웨어 무작위 숫자 생성기를 사용할 수 없는 경우 소프트웨어 기반 솔루션을 사용하여 엔트로피 풀 새로 고침 속도를 늘릴 수 있습니다. Linux에서 제공하는 이러한 소프트웨어 솔루션 [!DNL haveged] (HArdware Volatile Entorpy Gathering and Expansion 데몬)

## 사용 가능한 엔트로피 결정 {#section_686B311FE6144566B6939E9F20915ADC}

예기치 않은 지연 동안 지정된 서버의 엔트로피 풀에서 사용 가능한 비트 수를 확인하려면 다음 명령을 실행하십시오.

```
cat /proc/sys/kernel/random/entropy_avail 
```

엔트로피가 많은 건강한 리눅스 시스템은 4,096비트의 엔트로피가 될 것이다. 반환된 값이 200보다 작으면 시스템의 엔트로피가 매우 낮습니다.
