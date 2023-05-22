---
description: 라이센스 서버에서 구성 및 로그 파일의 위치를 제어하도록 구성할 수 있는 몇 가지 Java 시스템 속성이 있습니다.
title: Java 시스템 속성
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java 시스템 속성{#java-system-properties}

라이센스 서버에서 구성 및 로그 파일의 위치를 제어하도록 구성할 수 있는 몇 가지 Java 시스템 속성이 있습니다.

다음 Java 시스템 속성을 선택적으로 구성할 수 있습니다.

* *`LicenseServer.ConfigRoot`* — 라이센스 서버의 구성 파일이 포함된 디렉토리의 이름입니다.

   다음을 참조하십시오 *라이선스 서버 구성 파일* 이러한 파일의 내용에 대한 자세한 내용은 을 참조하십시오. 구성되지 않은 경우 기본값은 입니다. `CATALINA_BASE/licenseserver`.

* *LicenseServer.Logroot* — 이름 [!DNL logs] 라이선스 서버 응용 프로그램 로그가 있는 디렉터리입니다. 이 디렉토리의 이름을 수정하지 않은 경우 이 디렉토리의 이름은 로 구성됩니다. *LicenseServer.ConfigRoot* 기본적으로.

를 사용하는 경우 [!DNL catalina.bat] 또는 [!DNL catalina.sh] Tomcat을 시작하려면 다음을 사용하여 시스템 속성을 구성할 수 있습니다. `JAVA_OPTS` 환경 변수입니다. 사용자가 구성하는 모든 Java 옵션은 Tomcat이 시작될 때 자동으로 적용됩니다.

예를 들어 다음을 구성할 수 있습니다 `JAVA_OPTS` 환경 변수를 다음과 같이 지정합니다.

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
