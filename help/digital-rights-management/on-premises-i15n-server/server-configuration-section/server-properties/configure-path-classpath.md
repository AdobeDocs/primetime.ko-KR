---
title: 경로 및 클래스 경로 구성
description: 경로 및 클래스 경로 구성
copied-description: true
exl-id: e6e9f837-4e3d-43e1-971d-3fa0ccaeff39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 경로 및 클래스 경로 구성{#configure-the-path-and-classpath}

다음 [!DNL flashaccess.war] 다음 포함 [!DNL jsafeWithNative.jar]: Crypto-J 라이브러리입니다. 후자의 경우 암호화 작업을 수행하려면 추가 기본 라이브러리가 필요합니다.

1. 기본 추가 [!DNL jsafe] 라이브러리를 경로에 추가합니다.

   * **Linux / [!DNL libjsafe.so] -** 다음 포함 디렉터리 [!DNL libjsafe.so] 은(는) 경로에 있어야 합니다(다른 플랫폼에서도 기본 Crypto-J 라이브러리를 사용할 수 있음). 예를 들어, 을 설정합니다. [!DNL libjsafe.so] 날짜 `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** Windows의 상대 [!DNL libjsafe.so] 적절함 [!DNL jsafe.dll].
   이러한 라이브러리는 다음에서 사용할 수 있습니다. [!DNL thirdparty] 라이브러리 폴더입니다.
1. 다음 중 하나를 넣습니다. [!DNL adobe-flashaccess-certs] 클래스 경로에 있는 jar 파일입니다.

       이 JAR 파일은 WAR 파일에 포함되지 않습니다. 클래스 경로에 명시적으로 추가해야 합니다.
   
   * 개발 서버 - 만 사용해야 함 [!DNL adobe-flashaccess-certs-prerelease.jar].
   * 프로덕션 서버 - 만 사용해야 함 [!DNL adobe-flashaccess- certs.jar]

배포에는 다음이 포함됩니다. [!DNL shared] jar 파일과 사전 구성된 폴더가 모두 포함된 폴더 [!DNL AdobeInitial.properties] 파일. Adobe은 다음 항목을 `common.loader` 를 통해 [!DNL catalina.properties] 파일. 예:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
