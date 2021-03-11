---
title: 성능 조정
description: 성능 조정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 성능 조정{#performance-tuning}

성능을 높이려면 다음 팁을 사용합니다.

* 네트워크 HSM 사용 속도는 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있습니다.
* 성능을 향상시키려면 SDK의 &quot;thirdparty/cryptoj&quot; 폴더에 있는 플랫폼 특정 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 선택적으로 활성화할 수 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가하십시오.

   >[!NOTE]
   >
   >동일한 Tomcat 인스턴스에서 여러 웹 애플리케이션을 실행하고 경로에 `jsafe.dll`이 있는 경우 로드되는 첫 번째 웹 애플리케이션만 `jsafe.dll` 라이브러리를 로드할 수 있습니다. 따라서 기본 지원을 통해 첫 번째 웹 애플리케이션만 혜택을 받을 수 있습니다. 이러한 경우 모든 웹 응용 프로그램의 성능을 향상하려면 WAR 파일 외부에 `cryptoj.jar`을(를) 배치합니다. 예를 들어 `<tomcat_installation_folder>/lib` 디렉토리에 있습니다.

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제에 비해 훨씬 향상된 성능을 제공합니다.

