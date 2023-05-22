---
title: Adobe 액세스 배포
description: Adobe 액세스 배포
copied-description: true
exl-id: bebf02d5-897e-4007-8c5c-1c91186fdc51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# Adobe 액세스 배포 {#deploy-adobe-access}

Adobe 액세스 SDK의 주요 장점은 Tomcat과 같은 Java™ 애플리케이션 서버나 서블릿 컨테이너에 설치할 수 있다는 것입니다. JDK™ 1.5 이상도 필요합니다. 소프트웨어 요구 사항에 대한 자세한 내용은 액세스 SDK 플랫폼 요구 사항 Adobe 을 참조하십시오. [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Adobe 액세스를 배포하는 높은 수준의 단계는 다음과 같습니다.

1. Adobe 액세스 SDK를 설치하고 구성합니다.
1. Adobe에서 디지털 인증서를 받습니다.
1. SDK를 사용하여 라이선스 서버를 만들거나 보호된 스트리밍을 위해 Adobe Access Server을 배포합니다.
1. 컨텐츠 패키징 및 정책 관리 도구를 만들어 컨텐츠를 패키징하거나, 제공된 컨텐츠 준비 도구를 사용하거나, Adobe HTTP Dynamic Streaming 패키징 중 하나에 라이선스를 부여합니다.
1. 콘텐츠에 대한 사용 규칙을 정의하고 이러한 규칙을 지원하는 정책을 만듭니다.
1. 패키징 및 정책 관리 도구를 사용하여 콘텐츠를 패키징합니다.
1. 소비자가 Flash Player 또는 Adobe AIR을 사용하여 보호된 콘텐츠를 볼 수 있는 비디오 애플리케이션을 개발하거나 Adobe 액세스를 지원하는 기존 OVP(온라인 비디오 플랫폼)를 사용할 수 있습니다.
1. 웹 사이트에 Flash Player과 함께 사용할 SWF 파일을 배포하거나 Adobe AIR 설치 관리자를 게시하여 다운로드합니다.

이러한 단계는 다음 섹션에서 추가 정보가 포함된 다른 문서를 참조하여 확장되었습니다.

## 64비트 운영 체제에 배포 {#deploying-on-a-bit-operating-system}

64비트 버전의 RedHat이나 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 뛰어난 성능을 제공합니다.

## Adobe 액세스 SDK 설치 {#install-adobe-access-sdk}

Adobe 액세스 SDK는 JAR(Java Archive) 파일로 제공됩니다. Adobe 액세스 설치에 대한 자세한 내용은 *컨텐츠 보호를 위해 Adobe 액세스 SDK 사용*&#x200B;및&#x200B;*보안 배포 지침*.

## 라이센스 서버 구현 {#implement-a-license-server}

Adobe 액세스 SDK를 사용하여 라이선스 서버를 만들어야 합니다. Adobe 액세스를 사용하여 콘텐츠를 보호하는 경우 라이선스 서버에서 소비자에게 라이선스를 발급할 때까지 해당 콘텐츠를 볼 수 없습니다. ID 기반 라이센스를 사용하는 경우 암호 기반 인증을 통해 권한이 부여된 소비자만 컨텐츠를 열고 볼 수 있습니다.

라이선스 서버를 구현할 때는 Adobe에서 필요한 디지털 인증서를 받아야 합니다. 인증서 요청에 대한 자세한 지침은 Adobe 액세스 인증서 등록 문서를 참조하십시오.

라이센스 서버 구현 및 디지털 인증서 취득에 대한 자세한 내용은 콘텐츠 보호를 위한 Adobe 액세스 SDK 사용을 참조하십시오.*

## 컨텐츠 패키징 및 정책 관리 도구 만들기 {#create-content-packaging-and-policy-management-tools}

Adobe 액세스 SDK를 사용하여 콘텐츠 패키징 및 정책 관리 도구를 만들 수 있습니다. 관리자는 정책 관리 API를 사용하여 정책을 만들고, 세부 정보를 보고, 업데이트할 수 있습니다. 패키징 API는 정책을 FLV 또는 F4V 파일에 임베드하고 컨텐츠 암호화 키를 사용하여 파일을 암호화합니다.

Adobe 액세스 SDK에는 참조 구현( [!DNL AdobePackager.jar])를 참조하십시오. [!DNL AdobePolicyManager.jar]).

콘텐츠 패키징 및 정책 관리 도구 만들기에 대한 자세한 내용은 다음을 참조하십시오. *컨텐츠 보호를 위해 Adobe 액세스 SDK 사용*.

## 정책 만들기 및 콘텐츠 패키지 {#create-policies-and-package-content}

SDK에서 지원하는 사용 규칙을 사용하여 조직의 비즈니스 모델을 지원하는 정책을 정의하고 만든 다음 해당 정책을 사용하여 콘텐츠를 패키징해야 합니다. 패키지화하는 동안 콘텐츠에 정책이 적용되면 콘텐츠가 아무리 널리 배포되어도 콘텐츠에 대한 제어를 유지할 수 있습니다.

Adobe 액세스의 정책은 다음을 포함하여 광범위한 다양한 사용 규칙을 지원합니다.

* 소비자가 콘텐츠를 시청하기 시작한 후 라이선스가 유효한 일 수를 지정합니다.
* 라이선스 캐싱 허용.
* 콘텐츠에 액세스할 수 있는 클라이언트 런타임 및 버전 지정(예: 사용자에게 특정 Adobe AIR 애플리케이션이나 특정 버전의 Flash Player이 있어야 함).
* 소비자가 보호된 콘텐츠를 보기 전에 사용자 이름과 암호를 사용하여 자신을 인증하도록 하거나 익명 액세스를 허용합니다.

콘텐츠 패키징에 대한 자세한 내용은 *콘텐츠 보호*. 사용 규칙 및 사용 규칙이 지원하는 비즈니스 모델에 대한 자세한 내용은 다음을 참조하십시오. *사용 규칙*.

## 비디오 재생을 위한 애플리케이션 개발 {#develop-applications-for-video-playback}

소비자가 콘텐츠에 액세스하고 콘텐츠를 볼 수 있도록 하려면 Flash Player 또는 Adobe AIR을 사용하여 비디오 재생 애플리케이션을 개발하십시오. 비디오 재생 애플리케이션을 개발한 후에는 소비자에게 배포해야 합니다. Flash Player을 사용하여 애플리케이션을 개발하는 경우 조직의 웹 사이트에서 호스팅합니다. Adobe® AIR®을 사용하여 애플리케이션을 개발하는 경우 소비자가 컴퓨터에 애플리케이션을 다운로드하여 설치할 수 있도록 AIR 애플리케이션 설치 관리자를 게시하십시오.

Adobe 액세스에 사용할 사용자 지정 비디오 재생 애플리케이션 개발에 대한 자세한 내용은 의 &quot;비디오로 작업&quot; 장을 참조하십시오. [ActionScript 3.0 개발자 안내서](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*, *해당 [Adobe 비디오 기술 센터](https://www.adobe.com/devnet/video/)및 Open Source Media Framework
