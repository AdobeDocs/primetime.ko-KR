---
description: Adobe® Access™을 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 서드파티 클래스가 들어 있는 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems Incorporated에서 인증서를 요청합니다. 클라이언트와 서버 간의 통신, 라이센스 및 패키지 콘텐츠의 무결성을 보호하는 데 사용되는 여러 자격 증명이 발급됩니다.
title: 개발 환경 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# SDK 설정 {#setting-up-the-sdk}

Adobe® Access™을 설정하려면 DVD에서 파일을 복사하십시오. 이러한 파일에는 코드, 인증서 및 서드파티 클래스가 들어 있는 JAR 파일이 포함되어 있습니다. 또한 Adobe Systems Incorporated에서 인증서를 요청합니다. 클라이언트와 서버 간의 통신, 라이센스 및 패키지 콘텐츠의 무결성을 보호하는 데 사용되는 여러 자격 증명이 발급됩니다.

Adobe 액세스 SDK는 두 가지 유형으로 사용할 수 있습니다.
* ADOBE ACCESS CORE SDK
* ADOBE ACCESS PROFESSIONAL SDK

다음 표는 Adobe 액세스 SDK의 기본 비교를 보여 줍니다.

| 기능 | ADOBE ACCESS CORE SDK | ADOBE ACCESS PROFESSIONAL SDK |
|---|---|---|
| Flash Access 2.0 기능 | 사용 가능 | 사용 가능 |
| 키 회전 | - | 사용 가능 |
| 도메인 지원 | 사용 가능 | 사용 가능 |
| 향상된 라이선스 체인 | 사용 가능 | 사용 가능 |
| 동기화 메시지 | 사용 가능 | 사용 가능 |
| 라이선스 사전 생성 | 사용 가능 | 사용 가능 |
| 임베드된 라이센스 | 사용 가능 | 사용 가능 |

## 개발 환경 설정 {#setting-up-the-development-environment}

DVD에서 개발 환경 및 Java 클래스 경로에서 사용할 다음 SDK 파일을 복사합니다.

* adobe-flashaccess-certs.jar(Adobe 루트 인증서 포함)
* adobe-flashaccess-sdk.jar (Adobe Access Core SDK 클래스 포함)
* adobe-flashaccess-sdk-pro.jar(Adobe Access Professional SDK 클래스 포함, Professional 기능에만 필요)

SDK의 &quot;thirdparty&quot; 폴더에 있는 DVD에 있는 다음 타사 JAR 파일도 필요합니다.

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

성능을 향상시키기 위해 SDK의 &quot;thirdparty/cryptoj&quot; 폴더에 있는 플랫폼별 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 활성화할 수도 있습니다. 기본 지원을 활성화하려면 플랫폼의 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가합니다. 이러한 라이브러리의 32비트 및 64비트 버전이 제공됩니다. (64비트 버전은 64비트 OS가 있고 64비트 Java 버전을 실행 중인 경우에만 사용해야 합니다.)

또한 SDK의 선택적 요소는 adobe-flashaccess-lcrm.jar입니다. 이 파일은 FMRMS(Adobe Flash 미디어 Rights Management 서버) 1.x 호환성과 관련된 기능에만 필요합니다. 이전에 FMRMS 1.x를 배포했으며 FMRMS로 보호된 콘텐츠를 다시 패키징하지 않으려면 라이선스 서버에 지원을 추가하여 이전 콘텐츠와 클라이언트를 처리할 수 있도록 해야 합니다.
