---
description: 참조 구현 서버를 사용하면 Adobe Primetime DRM Java SDK의 모든 기능을 사용하는 완전한 기능을 갖춘 라이센스 서버를 만들 수 있습니다.
title: 라이센스 서버
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 라이센스 서버 {#license-server}

참조 구현 서버를 사용하면 Adobe Primetime DRM Java SDK의 모든 기능을 사용하는 완전한 기능을 갖춘 라이센스 서버를 만들 수 있습니다.

이 구현에서 사용자는 데이터베이스의 사용자 항목을 기반으로 인증됩니다. 이 서버에는 라이선스 발급을 위한 데모 비즈니스 로직이 포함되어 있으며 Flash Media Rights Management Server 1.0 및 1.5에 대한 호환성 지원을 제공합니다.

## 라이센스 서버 요구 사항 {#license-server-requirements}

라이센스 서버 요구 사항:

* Tomcat 6.0 이상 설치
* 데이터베이스 설치(예: MySQL([!DNL Third Party\MySQL]의 DVD에서 사용 가능)
* Java 1.6 이상이 설치되어 있는지 확인합니다.
* 샘플 빌드 스크립트를 실행하려면 Ant 1.8 이상이 있는지 확인합니다

Tomcat 및 MySQL을 설치한 후 Adobe에 필수 DRM 자격 증명 세트에 대해 문의하십시오.

## 라이센스 서버 {#build-the-license-server} 구축

>[!NOTE]
>
>라이센스 서버를 구축하는 것은 소스 코드를 수정하려는 경우에만 필요합니다. 평가를 위해 WAR 파일을 배송된 상태로 간편하게 사용할 수 있습니다.

참조 구현 라이센스 서버에는 비즈니스 요구에 맞게 라이센스 서버를 사용자 지정할 수 있는 Ant 빌드 스크립트( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)와 함께 모든 라이센스 서버 소스 코드( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)가 포함되어 있습니다.

1. Ant 빌드 스크립트를 수정하여 Primetime DRM SDK, Tomcat, MySQL 및 Log4J의 위치를 지정합니다.

   텍스트 편집기에서 [!DNL build-refimpl.xml] 파일을 열고 다음 속성 값을 설정합니다.

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Ant 빌드 스크립트가 있는 디렉토리에서 `all` 속성으로 Ant 빌드 스크립트를 실행합니다.

   ```
   ant -f build-refimpl.xml all
   ```

   Ant 빌드 스크립트는 서버 WAR 파일을 포함하는 [!DNL refimpl-build/wars] 디렉토리를 만듭니다.
