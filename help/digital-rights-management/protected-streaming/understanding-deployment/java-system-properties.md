---
description: 구성 및 로그 파일의 위치를 제어하기 위해 라이센스 서버에서 구성할 수 있는 여러 Java 시스템 속성이 있습니다.
title: Java 시스템 속성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Java 시스템 속성{#java-system-properties}

구성 및 로그 파일의 위치를 제어하기 위해 라이센스 서버에서 구성할 수 있는 여러 Java 시스템 속성이 있습니다.

선택적으로 다음 Java 시스템 속성을 구성할 수 있습니다.

* *`LicenseServer.ConfigRoot`* — 라이센스 서버의 구성 파일을 포함하는 디렉토리의 이름입니다.

   이러한 파일의 내용에 대한 자세한 내용은 *라이센스 서버 구성 파일*&#x200B;을 참조하십시오. 구성하지 않으면 기본값은 `CATALINA_BASE/licenseserver`입니다.

* *LicenseServer.LogRoot* —  [!DNL logs] 라이센스 서버 응용 프로그램 로그가 있는 디렉토리의 이름입니다. 이 디렉토리의 이름을 수정하지 않은 경우 이 디렉토리의 이름이 기본적으로 *LicenseServer.ConfigRoot*&#x200B;로 구성됩니다.

[!DNL catalina.bat] 또는 [!DNL catalina.sh] 파일을 사용하여 Tomcat을 시작하는 경우 `JAVA_OPTS` 환경 변수를 사용하여 시스템 속성을 구성할 수 있습니다. 구성하는 모든 Java 옵션은 Tomcat이 시작되면 자동으로 적용됩니다.

예를 들어 다음과 같이 `JAVA_OPTS` 환경 변수를 구성할 수 있습니다.

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

