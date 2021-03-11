---
title: 경로 및 클래스 경로 구성
description: 경로 및 클래스 경로 구성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 경로 및 클래스 경로 구성{#configure-the-path-and-classpath}

[!DNL flashaccess.war]에는 Crypto-J 라이브러리인 [!DNL jsafeWithNative.jar]이 포함되어 있습니다. 암호화 작업을 수행하려면 기본 라이브러리가 추가로 필요합니다.

1. 경로에 기본 [!DNL jsafe] 라이브러리를 추가합니다.

   * **Linux /  [!DNL libjsafe.so] -** 포함된 디렉토리는 경로에  [!DNL libjsafe.so] 있어야 합니다(기본 Crypto-J 라이브러리는 다른 플랫폼에도 사용할 수 있음). 예를 들어 `LD_LIBRARY_PATH`에 [!DNL libjsafe.so]을 설정합니다.

   * **Windows /  [!DNL jsafe.dll] -** Windows에서 사용할 대상 [!DNL libjsafe.so] 이 적절합니다 [!DNL jsafe.dll].
   이러한 라이브러리는 [!DNL thirdparty] 라이브러리 폴더에서 사용할 수 있습니다.
1. [!DNL adobe-flashaccess-certs] jar 파일 중 하나를 클래스 경로에 넣습니다.

       이 JAR 파일은 WAR 파일에 포함되지 않습니다.클래스 경로에 명시적으로 추가해야 합니다.
   
   * 개발 서버 - [!DNL adobe-flashaccess-certs-prerelease.jar]만 사용해야 합니다.
   * 프로덕션 서버 - [!DNL adobe-flashaccess- certs.jar]만 사용해야 함

배포에는 미리 구성된 [!DNL AdobeInitial.properties] 파일과 jar 파일을 모두 포함하는 [!DNL shared] 폴더가 포함되어 있습니다. Adobe에서는 [!DNL catalina.properties] 파일을 통해 `common.loader`에 이러한 항목을 추가하는 것이 좋습니다. 예:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


