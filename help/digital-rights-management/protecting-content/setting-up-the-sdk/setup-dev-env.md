---
description: Primetime DRM을 설정하려면 DVD에서 파일을 복사합니다. 이러한 파일에는 코드, 인증서 및 서드파티 클래스를 포함하는 JAR 파일이 포함됩니다. 또한 Adobe Systems, Incorporated에 인증서를 요청해야 합니다. 그런 다음 Adobe에서 패키지화된 콘텐츠의 무결성, 라이센스 및 클라이언트와 서버 간 통신을 보호하는 데 사용하는 여러 자격 증명을 발급합니다.
title: 개발 환경 설정
exl-id: c10f85b6-84bc-444f-9001-f49dc88cf99c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 개발 환경 설정 {#set-up-your-development-environment}

Primetime DRM을 설정하려면 DVD에서 파일을 복사합니다. 이러한 파일에는 코드, 인증서 및 서드파티 클래스를 포함하는 JAR 파일이 포함됩니다. 또한 Adobe Systems, Incorporated에 인증서를 요청해야 합니다. 그런 다음 Adobe에서 패키지화된 콘텐츠의 무결성, 라이센스 및 클라이언트와 서버 간 통신을 보호하는 데 사용하는 여러 자격 증명을 발급합니다.

Adobe은 DVD에 Primetime DRM SDK를 제공합니다.

1. [!DNL]에서 다음 파일 복사 [DRM]/SDK/]를 Java 클래스 경로에 있는 개발 시스템에 추가합니다.

   * [!DNL adobe-flashaccess-certs.jar] - Adobe 루트 인증서 포함
   * [!DNL adobe-flashaccess-sdk.jar] - Primetime DRM 코어 SDK 클래스 포함
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Professional 기능에만 필요한 Primetime DRM Professional SDK 클래스 포함

1. [!DNL]에서 다음 파일 복사 [DRM]/SDK/thirdparty] 를 참조하십시오.

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

1. (선택 사항) 성능을 향상시키기 위해 [!DNL에서 적절한 플랫폼별 라이브러리를 복사하여 암호화 작업에 대한 기본 지원을 활성화할 수 있습니다 [DRM]/SDK/thirdparty/cryptoj/] 를 개발 시스템에 추가합니다(해당 위치를 경로에 배치해야 함).

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >이러한 라이브러리의 32비트 및 64비트 버전을 사용할 수 있습니다. 64비트 OS가 있고 64비트 버전의 Java를 실행하는 경우에만 64비트 버전을 사용해야 합니다.

1. (선택 사항) Adobe Flash Rights Management FMRMS(Media Media Server) 1.x 호환성과 관련된 기능을 보려면 를 복사합니다. `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 를 개발 시스템에 추가합니다.

   이전에 FMRMS 1.x를 배포했으며 FMRMS로 보호된 콘텐츠를 다시 패키징하지 않으려는 경우에만 이 배포합니다. 이 경우 라이선스 서버에서 이전 콘텐츠 및 클라이언트를 관리할 수 있도록 이 지원을 라이선스 서버에 추가해야 합니다.
