---
title: 성능 조정
description: 성능 조정
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 성능 조정{#performance-tuning}

다음 팁을 사용하여 성능을 높이십시오.

* 네트워크 HSM을 사용하는 것은 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있다.
* 성능을 향상시키기 위해 SDK의 &quot;thirdparty/cryptoj&quot; 폴더에 있는 플랫폼별 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 활성화할 수도 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가합니다.

  >[!NOTE]
  >
  >동일한 Tomcat 인스턴스에서 여러 웹 응용 프로그램을 실행하고 `jsafe.dll` 경로에서 로드되는 첫 번째 웹 애플리케이션만 `jsafe.dll` 라이브러리입니다. 따라서 첫 번째 웹 애플리케이션만 기본 지원의 이점을 얻을 수 있습니다. 이러한 경우 모든 웹 애플리케이션의 성능을 향상시키려면 다음을 수행하십시오. `cryptoj.jar`WAR 파일 외부. 예를 들어, `<tomcat_installation_folder>/lib` 디렉토리.

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 뛰어난 성능을 제공합니다.
