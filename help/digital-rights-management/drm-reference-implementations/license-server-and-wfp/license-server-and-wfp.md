---
description: 참조 구현 서버를 사용하면 Adobe Primetime DRM Java SDK의 모든 기능을 사용하는 완전한 기능을 갖춘 라이선스 서버를 만들 수 있습니다.
title: 라이선스 서버
exl-id: a928b7ac-9191-4b8c-b038-eb92a09286fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 라이선스 서버 {#license-server}

참조 구현 서버를 사용하면 Adobe Primetime DRM Java SDK의 모든 기능을 사용하는 완전한 기능을 갖춘 라이선스 서버를 만들 수 있습니다.

이 구현에서 사용자는 데이터베이스의 사용자 항목을 기반으로 인증됩니다. 이 서버에는 라이센스 발급을 위한 데모 비즈니스 로직이 포함되어 있으며 Flash 미디어 Rights Management 서버 1.0 및 1.5에 대한 호환성 지원을 제공합니다.

## 라이선스 서버 요구 사항 {#license-server-requirements}

라이선스 서버 요구 사항:

* Tomcat 6.0 이상 설치
* 데이터베이스(예: DVD에서 사용 가능한 MySQL)를 [!DNL Third Party\MySQL])
* Java 1.6 이상이 설치되어 있는지 확인합니다.
* 샘플 빌드 스크립트를 실행하려면 Ant 1.8 이상이 있어야 합니다

Tomcat 및 MySQL을 설치한 후 필요한 DRM 자격 증명 세트에 대해 Adobe에 문의하십시오.

## 라이선스 서버 구축 {#build-the-license-server}

>[!NOTE]
>
>소스 코드를 수정하려는 경우에만 라이선스 서버를 빌드해야 합니다. 평가를 위해 WAR 파일을 배송된 대로 사용할 수 있습니다.

참조 구현 라이선스 서버에는 모든 라이선스 서버 소스 코드( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), Ant 빌드 스크립트( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)를 사용하여 비즈니스 요구 사항에 맞게 라이선스 서버를 사용자 지정할 수 있습니다.

1. Ant 빌드 스크립트를 수정하여 Primetime DRM SDK, Tomcat, MySQL 및 Log4J의 위치를 지정합니다.

   를 엽니다. [!DNL build-refimpl.xml] 파일을 텍스트 편집기에 저장하고 다음 속성 값을 설정합니다.

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 다음을 사용하여 Ant 빌드 스크립트 실행 `all` 속성, Ant 빌드 스크립트가 있는 디렉터리에서 참조할 수 있습니다.

   ```
   ant -f build-refimpl.xml all
   ```

   Ant 빌드 스크립트는 [!DNL refimpl-build/wars] 서버 WAR 파일이 포함된 디렉터리입니다.
