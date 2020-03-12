---
seo-title: 경로 및 클래스 경로 구성
title: 경로 및 클래스 경로 구성
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 경로 및 클래스 경로 구성{#configure-the-path-and-classpath}

Crypto- [!DNL flashaccess.war] J 라이브러리인 포함 [!DNL jsafeWithNative.jar]사항 암호 작업을 수행하려면 추가 기본 라이브러리가 필요합니다.

1. 경로에 기본 [!DNL jsafe] 라이브러리를 추가합니다.

   * **Linux /[!DNL libjsafe.so]-** 포함하는 디렉토리는 경로에 [!DNL libjsafe.so] 있어야 합니다(기본 Crypto-J 라이브러리는 다른 플랫폼에서도 사용할 수 있음). 예를 들어 [!DNL libjsafe.so] on을 `LD_LIBRARY_PATH`설정합니다.

   * **Windows /[!DNL jsafe.dll]- Windows** 의 [!DNL libjsafe.so] 대응 방법은 적절합니다 [!DNL jsafe.dll].
   이러한 라이브러리는 [!DNL thirdparty] 라이브러리 폴더에서 사용할 수 있습니다.
1. jar 파일 중 하나를 클래스 경로에 [!DNL adobe-flashaccess-certs] 넣습니다.

       이 JAR 파일은 WAR 파일에 포함되어 있지 않습니다.클래스 경로에 명시적으로 추가해야 합니다.
   
   * 개발 서버 - 사용해야 [!DNL adobe-flashaccess-certs-prerelease.jar]합니다.
   * 프로덕션 서버 - [!DNL adobe-flashaccess- certs.jar]

배포에는 jar 파일과 미리 구성된 [!DNL shared] [!DNL AdobeInitial.properties] 파일이 모두 포함된 폴더가 포함됩니다. Adobe에서는 이러한 항목을 파일을 `common.loader` 통해 에 추가하는 것이 좋습니다 [!DNL catalina.properties] . 예:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


