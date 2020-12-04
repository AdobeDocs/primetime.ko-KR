---
seo-title: 경로 및 클래스 경로 구성
title: 경로 및 클래스 경로 구성
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 경로 및 클래스 경로 구성{#configure-the-path-and-classpath}

[!DNL flashaccess.war]에는 Crypto-J 라이브러리인 [!DNL jsafeWithNative.jar]이 포함되어 있습니다. 암호화 작업을 수행하려면 기본 라이브러리가 추가로 필요합니다.

1. 경로에 기본 [!DNL jsafe] 라이브러리를 추가합니다.

   * **Linux /  [!DNL libjsafe.so] -** The directory containing  [!DNL libjsafe.so] must be on the Path (native Crypto-J libraries also available for other platform). 예를 들어 `LD_LIBRARY_PATH`에 [!DNL libjsafe.so]을 설정합니다.

   * **Windows /  [!DNL jsafe.dll] -** Windows [!DNL libjsafe.so] 에서 사용할 수  [!DNL jsafe.dll]있는 대상은 적절합니다.
   이러한 라이브러리는 [!DNL thirdparty] 라이브러리 폴더에서 사용할 수 있습니다.
1. [!DNL adobe-flashaccess-certs] jar 파일 중 하나를 클래스 경로에 넣습니다.

       이 JAR 파일은 WAR 파일에 포함되지 않습니다.클래스 경로에 명시적으로 추가해야 합니다.
   
   * 개발 서버 - [!DNL adobe-flashaccess-certs-prerelease.jar]만 사용해야 합니다.
   * 프로덕션 서버 - [!DNL adobe-flashaccess- certs.jar]만 사용해야 함

배포에는 jar 파일과 사전 구성된 [!DNL AdobeInitial.properties] 파일이 모두 포함된 [!DNL shared] 폴더가 포함됩니다. Adobe은 [!DNL catalina.properties] 파일을 통해 `common.loader`에 이러한 항목을 추가하는 것이 좋습니다. 예:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


