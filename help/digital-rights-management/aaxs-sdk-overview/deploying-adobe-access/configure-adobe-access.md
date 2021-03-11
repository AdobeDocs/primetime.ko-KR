---
title: Adobe 액세스 배포
description: Adobe 액세스 배포
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Adobe 액세스 배포 {#deploy-adobe-access}

Adobe 액세스 SDK의 주요 이점은 Tomcat과 같은 Java™ 응용 프로그램 서버 또는 서블릿 컨테이너에 설치할 수 있다는 것입니다. 또한 JDK™ 1.5 이상이 필요합니다. 소프트웨어 요구 사항에 대한 자세한 내용은 Adobe 액세스 SDK 플랫폼 요구 사항을 참조하십시오.[:https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Adobe 액세스를 배포하는 고급 단계는 다음과 같습니다.

1. Adobe 액세스 SDK를 설치하고 구성합니다.
1. Adobe에서 디지털 인증서를 획득합니다.
1. SDK를 사용하여 라이센스 서버를 만들거나 스트리밍 보호를 위해 Adobe Access Server을 배포합니다.
1. 컨텐츠 패키징 및 정책 관리 툴을 제작하여 컨텐츠를 패키지화하고 제공된 컨텐츠 준비 툴을 사용하거나 Adobe HTTP Dynamic Streaming 패키지 중 하나에 라이선스를 부여할 수 있습니다.
1. 콘텐츠에 대한 사용 규칙을 정의하고 해당 규칙을 지원하는 정책을 만듭니다.
1. 패키징 및 정책 관리 툴을 사용하여 컨텐츠를 패키지화할 수 있습니다.
1. Flash Player 또는 Adobe AIR을 사용하여 소비자가 보호된 컨텐츠를 볼 수 있는 비디오 애플리케이션을 개발하거나 Adobe 액세스를 지원하는 기존의 OVP(온라인 비디오 플랫폼)를 사용할 수 있습니다.
1. Flash Player에 사용할 SWF 파일을 웹 사이트에 배포하거나 Adobe AIR 설치 프로그램을 게시하여 다운로드할 수 있습니다.

이러한 단계는 다음 섹션에서 확장되며 추가 정보가 포함된 다른 문서에 대한 참조가 포함됩니다.

## 64비트 운영 체제 {#deploying-on-a-bit-operating-system}에 배포

64비트 버전의 RedHat 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 향상된 성능을 제공합니다.

## Adobe 액세스 SDK {#install-adobe-access-sdk} 설치

Adobe 액세스 SDK는 JAR(Java Archive) 파일로 제공됩니다. Adobe 액세스 설치에 대한 자세한 내용은 *콘텐트 보호를 위한 Adobe 액세스 SDK 사용* 및&#x200B;*보안 배포 지침*&#x200B;을 참조하십시오.

## 라이센스 서버 구현 {#implement-a-license-server}

Adobe 액세스 SDK를 사용하는 경우 라이센스 서버를 만들어야 합니다. Adobe 액세스를 사용하여 콘텐트를 보호하는 경우 라이센스 서버가 고객에게 라이센스를 발급하기 전까지 콘텐트를 볼 수 없습니다. ID 기반 라이센스를 사용하는 경우 암호 기반 인증을 통해 인증된 소비자의 만이 컨텐츠를 열고 볼 수 있습니다.

라이센스 서버를 구현할 때는 Adobe에서 필요한 디지털 인증서를 받아야 합니다. 인증서 요청에 대한 자세한 내용은 Adobe 액세스 인증서 등록 문서를 참조하십시오.

라이센스 서버 구현 및 디지털 인증서 획득에 대한 자세한 내용은* 컨텐트 보호를 위한 Adobe 액세스 SDK 사용을 참조하십시오.*

## 내용 패키징 및 정책 관리 도구 만들기 {#create-content-packaging-and-policy-management-tools}

Adobe 액세스 SDK를 사용하여 컨텐츠 패키징 및 정책 관리 도구를 만들 수 있습니다. 정책 관리 API를 사용하여 관리자는 정책을 만들고, 세부 사항을 보고, 업데이트할 수 있습니다. 패키징 API는 정책을 FLV 또는 F4V 파일에 포함하고 내용 암호화 키를 사용하여 파일을 암호화합니다.

Adobe 액세스 SDK에는 컨텐츠 패키징 및 정책 관리 도구의 예( [!DNL AdobePolicyManager.jar])를 제공하는 참조 구현( [!DNL AdobePackager.jar])이 포함되어 있습니다.

콘텐츠 패키징 및 정책 관리 도구 만들기에 대한 자세한 내용은 *콘텐츠 보호를 위한 Adobe 액세스 SDK 사용*&#x200B;을 참조하십시오.

## 정책 만들기 및 콘텐트 {#create-policies-and-package-content} 패키지

SDK에서 지원하는 사용 규칙을 사용하여 조직의 비즈니스 모델을 지원하는 정책을 정의하고 만든 다음 해당 정책을 사용하여 컨텐츠를 패키지화해야 합니다. 패키징 중에 컨텐트에 정책을 적용하면 컨텐츠가 얼마나 널리 배포되었는지에 관계없이 컨텐츠를 제어할 수 있습니다.

Adobe 액세스의 정책은 다음을 비롯한 다양한 사용 규칙을 지원합니다.

* 소비자가 컨텐츠를 시청하기 시작하면 라이센스가 유효한 일 수를 지정합니다.
* 라이선스 캐싱 허용.
* 콘텐트에 액세스할 수 있는 클라이언트 런타임 및 버전 지정(예: 사용자에게 특정 Adobe AIR 응용 프로그램이나 특정 Flash Player 버전이 있어야 함).
* 보호된 컨텐츠를 보거나 익명 액세스를 허용하기 전에 사용자가 사용자 이름과 암호를 사용하여 자신을 인증하도록 요구

콘텐츠 패키징에 대한 자세한 내용은 *콘텐츠 보호*&#x200B;를 참조하십시오. 사용 규칙 및 지원되는 비즈니스 모델에 대한 자세한 내용은 *사용 규칙*&#x200B;을 참조하십시오.

## 비디오 재생을 위한 애플리케이션 개발 {#develop-applications-for-video-playback}

사용자가 컨텐츠에 액세스하고 볼 수 있도록 하려면 Flash Player 또는 Adobe AIR을 사용하여 비디오 재생 응용 프로그램을 개발합니다. 비디오 재생 응용 프로그램을 개발한 후에는 소비자에게 배포해야 합니다. Flash Player을 사용하여 애플리케이션을 개발하는 경우 조직의 웹 사이트에서 호스팅하십시오. Adobe® AIR®를 사용하여 응용 프로그램을 개발하는 경우 사용자가 응용 프로그램을 다운로드하여 컴퓨터에 설치할 수 있도록 AIR 응용 프로그램 설치 프로그램을 게시합니다.

Adobe Access에서 사용할 사용자 정의 비디오 재생 응용 프로그램을 개발하는 방법에 대한 자세한 내용은 [ActionScript 3.0 개발자 안내서](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*, *a2/>Adobe 비디오 기술 센터](https://www.adobe.com/devnet/video/) 및 Open Source Media Framework의 &quot;비디오 작업&quot; 장을 참조하십시오.[