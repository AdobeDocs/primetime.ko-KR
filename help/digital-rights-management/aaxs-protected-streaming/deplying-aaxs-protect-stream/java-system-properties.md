---
title: Java 시스템 속성
description: Java 시스템 속성
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java 시스템 속성 {#java-system-properties}

라이센스 서버의 구성 및 로그 파일 위치를 수정하기 위해 다음 두 개의 Java 시스템 속성을 선택적으로 설정할 수 있습니다.

* *LicenseServer.ConfigRoot* — 라이센스 서버의 모든 구성 파일이 포함된 디렉토리입니다. 이러한 파일의 내용에 대한 자세한 내용은 &quot;[라이선스 서버 구성 파일](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. 설정하지 않으면 기본값은 입니다. *CATALINA_BASE/licenseserver*.
* *LicenseServer.Logroot* — 라이센스 서버 애플리케이션 로그가 기록되는 &quot;logs&quot; 폴더의 디렉토리입니다. 설정하지 않으면 기본값은 입니다. *LicenseServer.ConfigRoot*.

을 사용하는 경우 [!DNL catalina.bat] 또는 [!DNL catalina.sh] tomcat을 시작하려면 다음을 사용하여 이러한 시스템 속성을 쉽게 설정할 수 있습니다. `JAVA_OPTS` 환경 변수입니다. Tomcat을 시작할 때 여기에 설정된 모든 Java 옵션이 사용됩니다. 예를 들어 다음을 설정합니다.

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
