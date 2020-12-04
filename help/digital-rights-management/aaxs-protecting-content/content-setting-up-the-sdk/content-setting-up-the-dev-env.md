---
description: 사용할 Adobe® Access™를 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 들어 있는 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems Incorporated에서 인증서를 요청하십시오. 패키지된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하는 데 사용되는 여러 개의 자격 증명이 발급됩니다.
seo-description: 사용할 Adobe® Access™를 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 들어 있는 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems Incorporated에서 인증서를 요청하십시오. 패키지된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하는 데 사용되는 여러 개의 자격 증명이 발급됩니다.
seo-title: 개발 환경 설정
title: 개발 환경 설정
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# SDK {#setting-up-the-sdk} 설정

사용할 Adobe® Access™를 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 타사 클래스가 들어 있는 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems Incorporated에서 인증서를 요청하십시오. 패키지된 컨텐츠, 라이선스 및 클라이언트와 서버 간의 커뮤니케이션의 무결성을 보호하는 데 사용되는 여러 개의 자격 증명이 발급됩니다.

Adobe 액세스 SDK는 다음 두 가지 유형으로 사용할 수 있습니다.
* Adobe Access Core SDK
* Adobe Access Professional SDK

다음 표는 Adobe 액세스 SDK에 대한 기본 비교를 보여줍니다.

| 기능 | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Flash Access 2.0 기능 | 사용 가능 | 사용 가능 |
| 키 회전 | - | 사용 가능 |
| 도메인 지원 | 사용 가능 | 사용 가능 |
| 향상된 라이센스 체인 | 사용 가능 | 사용 가능 |
| 동기화 메시지 | 사용 가능 | 사용 가능 |
| 라이선스 사전 생성 | 사용 가능 | 사용 가능 |
| 포함된 라이선스 | 사용 가능 | 사용 가능 |

## 개발 환경 설정 {#setting-up-the-development-environment}

DVD에서 개발 환경 및 Java 클래스 경로에 사용할 다음 SDK 파일을 복사합니다.

* adobe-flashaccess-certs.jar(Adobe 루트 인증서 포함)
* adobe-flashaccess-sdk.jar(Adobe Access Core SDK 클래스 포함)
* adobe-flashaccess-sdk-pro.jar(Adobe Access Professional SDK 클래스 포함, Professional 기능에만 필요)

SDK의 &quot;타사&quot; 폴더에도 있는 다음 타사 JAR 파일이 필요합니다.

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

성능을 향상시키려면 SDK의 &quot;thirdparty/cryptoj&quot; 폴더에 있는 플랫폼 특정 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 선택적으로 활성화할 수 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가하십시오. 이러한 라이브러리의 32비트 및 64비트 버전이 제공됩니다. (64비트 버전은 64비트 OS가 있고 64비트 버전의 Java를 실행 중인 경우에만 사용해야 합니다.)

또한 SDK의 선택적 부분은 adobe-flashaccess-lcrm.jar입니다. 이 파일은 Adobe Flash 미디어 Rights Management 서버(FMRMS) 1.x 호환성과 관련된 기능에만 필요합니다. 이전에 FMRMS 1.x를 배포했지만 FMRMS로 보호된 컨텐츠를 다시 패키지하지 않으려는 경우 이전 컨텐츠 및 클라이언트를 처리할 수 있도록 라이센스 서버에 지원을 추가해야 합니다.
