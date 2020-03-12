---
description: Primetime DRM을 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 포함된 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems, Incorporated에서 인증서를 요청해야 합니다. 그런 다음 Adobe는 패키징된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하기 위해 사용하는 여러 개의 자격 증명을 발행합니다.
seo-description: Primetime DRM을 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 포함된 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems, Incorporated에서 인증서를 요청해야 합니다. 그런 다음 Adobe는 패키징된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하기 위해 사용하는 여러 개의 자격 증명을 발행합니다.
seo-title: 개발 환경 설정
title: 개발 환경 설정
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 개발 환경 설정 {#set-up-your-development-environment}

Primetime DRM을 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 포함된 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems, Incorporated에서 인증서를 요청해야 합니다. 그런 다음 Adobe는 패키징된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하기 위해 사용하는 여러 개의 자격 증명을 발행합니다.

Adobe는 DVD에서 Primetime DRM SDK를 제공합니다.

1. [!DNL DRM DVD/ [SDK]/]에서 Java 클래스 경로에 있는 개발 시스템으로 다음 파일을 복사합니다.

   * [!DNL adobe-flashaccess-certs.jar] - Adobe 루트 인증서 포함
   * [!DNL adobe-flashaccess-sdk.jar] - Primetime DRM 코어 SDK 클래스 포함
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Primetime DRM Professional SDK 클래스 포함, Professional 기능에만 필요

1. [!DNL DRM DVD/ [SDK]/타사]에서 개발 시스템으로 다음 파일을 복사합니다.

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (선택 사항) 성능을 향상시키기 위해 [!DNL DRM DVD/SDK/ [SDK]/thirdparty/cryptoj/]의 해당 플랫폼 전용 라이브러리를 개발 시스템으로 복사하여 암호화 작업에 대한 기본 지원을 활성화할 수 있습니다(경로 위치 지정).

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >이러한 라이브러리의 32비트 및 64비트 버전을 사용할 수 있습니다. 64비트 OS가 있고 64비트 버전의 Java를 실행하는 경우에만 64비트 버전을 사용해야 합니다.

1. (선택 사항) Adobe Flash Media Rights Management Server(FMRMS) 1.x 호환성 관련 기능을 사용하려면 개발 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 시스템에 복사합니다.

   이전에 FMRMS 1.x를 배포했지만 FMRMS로 보호된 컨텐츠를 다시 패키지하지 않으려는 경우에만 배포하십시오. 이 경우 이 지원을 라이센스 서버에 추가하여 이전 컨텐츠 및 클라이언트를 관리할 수 있습니다.
