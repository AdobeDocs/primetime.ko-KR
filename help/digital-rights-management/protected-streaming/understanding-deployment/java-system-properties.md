---
description: 라이센스 서버에서 구성 및 로그 파일의 위치를 제어하도록 구성할 수 있는 여러 Java 시스템 속성이 있습니다.
seo-description: 라이센스 서버에서 구성 및 로그 파일의 위치를 제어하도록 구성할 수 있는 여러 Java 시스템 속성이 있습니다.
seo-title: Java 시스템 속성
title: Java 시스템 속성
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Java 시스템 속성{#java-system-properties}

라이센스 서버에서 구성 및 로그 파일의 위치를 제어하도록 구성할 수 있는 여러 Java 시스템 속성이 있습니다.

다음과 같은 Java 시스템 속성을 구성할 수도 있습니다.

* *`LicenseServer.ConfigRoot`* — 라이센스 서버의 구성 파일을 포함하는 디렉토리의 이름입니다.

   이러한 파일의 내용에 대한 자세한 내용은 *라이센스 서버 구성 파일*&#x200B;을 참조하십시오. 구성하지 않으면 기본값은 `CATALINA_BASE/licenseserver`입니다.

* *LicenseServer.LogRoot* — 라이센스 서버 응용 프로그램 로그가 있는  [!DNL logs] 디렉토리의 이름입니다. 이 디렉터리 이름을 수정하지 않은 경우 이 디렉터리의 이름은 기본적으로 *LicenseServer.ConfigRoot*&#x200B;로 구성됩니다.

[!DNL catalina.bat] 또는 [!DNL catalina.sh] 파일을 사용하여 Tomcat을 시작하는 경우 `JAVA_OPTS` 환경 변수를 사용하여 시스템 속성을 구성할 수 있습니다. 구성하는 모든 Java 옵션은 Tomcat이 시작될 때 자동으로 적용됩니다.

예를 들어 다음과 같이 `JAVA_OPTS` 환경 변수를 구성할 수 있습니다.

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

