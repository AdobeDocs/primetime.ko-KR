---
seo-title: Adobe Primetime DRM 배포
title: Adobe Primetime DRM 배포
uuid: c14c2792-d207-4f39-b856-610520bdaa28
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime DRM 배포 {#configure-adobe-primetime-drm}

Adobe Primetime DRM SDK의 주요 이점은 Tomcat과 같은 Java™ 애플리케이션 서버 또는 서블릿 컨테이너에 설치할 수 있다는 것입니다. 또한 JDK™ 1.5 이상이 필요합니다. 소프트웨어 요구 사항에 대한 자세한 내용은 Primetime DRM SDK 플랫폼 요구 사항을 참조하십시오.https://www.adobe.com/products/flashaccess/systemreqs/ [](https://www.adobe.com/products/flashaccess/systemreqs/).

Primetime DRM을 배포하는 고급 단계는 다음과 같습니다.

1. Primetime DRM SDK 설치 및 구성
1. Adobe에서 디지털 인증서를 획득합니다.
1. SDK를 사용하여 라이선스 서버를 만들거나 보호된 스트리밍을 위해 Primetime DRM Server를 배포합니다.
1. 컨텐츠 패키징 및 정책 관리 툴을 만들어 컨텐츠를 패키지하거나 제공된 컨텐츠 준비 툴을 사용하거나 Adobe HTTP Dynamic Streaming 패키지 중 하나에 라이선스를 부여할 수 있습니다.
1. 컨텐츠에 대한 사용 규칙을 정의하고 해당 규칙을 지원하는 정책을 만듭니다.
1. 패키징 및 정책 관리 툴을 사용하여 컨텐츠를 패키지화할 수 있습니다.
1. 소비자가 Flash Player 또는 Adobe AIR를 사용하여 보호된 컨텐츠를 볼 수 있는 비디오 애플리케이션을 개발하거나 Primetime DRM을 지원하는 기존의 OVP(온라인 비디오 플랫폼)를 사용할 수 있습니다.
1. Flash Player와 함께 사용할 SWF 파일을 웹 사이트에 배포하거나 다운로드할 수 있도록 Adobe AIR 설치 프로그램을 게시할 수 있습니다.

이러한 단계는 다음 섹션에서 확장되며 추가 정보가 포함된 다른 문서에 대한 참조가 포함됩니다.

## 64비트 운영 체제에 배포{#deploying-on-a-bit-operating-system}

64비트 버전의 RedHat 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 향상된 성능을 제공합니다.

## Adobe Primetime DRM SDK 설치 {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK 파섹 Primetime DRM 설치에 대한 자세한 내용은 콘텐츠 보호 및 보안 배포 가이드라인을 위한 Adobe Primetime DRM SDK 사용을 참조하십시오.

## 라이센스 서버 구현 {#implement-a-license-server}

Adobe Primetime DRM SDK를 사용하려면 라이선스 서버를 만들어야 합니다. Primetime DRM을 사용하여 콘텐트를 보호하는 경우 라이센스 서버가 사용자에게 라이센스를 발급하기 전까지 콘텐트를 볼 수 없습니다. ID 기반 라이선스를 사용하는 경우 암호 기반 인증을 통해 인증된 사용자만 컨텐츠를 열고 볼 수 있습니다.

라이센스 서버를 구현할 때에는 Adobe로부터 필요한 디지털 인증서를 받아야 합니다. 인증서 요청에 대한 자세한 내용은 Primetime DRM 인증서 등록 문서를 참조하십시오.

라이선스 서버 구현 및 디지털 인증서 획득에 대한 자세한 내용은 콘텐츠 보호를 **위한 Adobe Primetime DRM SDK 사용을 참조하십시오.**

## 컨텐츠 패키징 및 정책 관리 툴 제작{#create-content-packaging-and-policy-management-tools}

Adobe Primetime DRM SDK를 사용하면 콘텐츠 패키징 및 정책 관리 툴을 만들 수 있습니다. 정책 관리 API를 통해 관리자는 정책을 만들고, 세부 사항을 보고, 업데이트할 수 있습니다. 패키징 API는 정책을 비디오 파일에 포함하고 컨텐츠 암호화 키를 사용하여 파일을 암호화합니다.

Primetime DRM SDK에는 콘텐츠 패키징 및 정책 관리 도구( [!DNL AdobePackager.jar][!DNL AdobePolicyManager.jar])의 예를 제공하는 참조 구현()이 포함되어 있습니다.

콘텐츠 패키징 및 정책 관리 도구 만들기에 대한 자세한 내용은 콘텐츠 보호를 **위한 Adobe Primetime DRM SDK 사용을 참조하십시오.**

## 정책 만들기 및 컨텐츠 패키지 {#create-policies-and-package-content}

SDK에서 지원하는 사용 규칙을 사용하여 조직의 비즈니스 모델을 지원하기 위한 정책을 정의 및 만든 다음 해당 정책을 사용하여 컨텐츠를 패키징해야 합니다. 패키징 중에 컨텐트에 정책이 적용되면 배포 범위에 상관없이 컨텐츠를 제어할 수 있습니다.

Adobe Primetime DRM의 정책은 다음을 비롯한 다양한 사용 규칙을 지원합니다.

* 소비자가 컨텐츠를 시청하기 시작하면 라이선스가 유효한 일 수를 지정합니다.
* 라이선스 캐싱 허용
* 컨텐츠를 액세스할 수 있는 클라이언트 런타임 및 버전 지정(예: 사용자는 특정 Adobe AIR 애플리케이션 또는 특정 버전의 Flash Player가 있어야 함)
* 보호된 콘텐츠를 보거나 익명 액세스를 허용하기 전에 사용자가 사용자 이름과 암호를 사용하여 자신을 인증하도록 합니다.

콘텐츠 패키징에 대한 자세한 내용은 콘텐츠 보호를 *참조하십시오*. 사용 규칙 및 지원되는 비즈니스 모델에 대한 자세한 내용은 사용 규칙을 *참조하십시오*.

## 비디오 재생을 위한 애플리케이션 개발 {#develop-applications-for-video-playback}

소비자가 컨텐츠에 액세스하여 볼 수 있도록 하려면 Flash Player 또는 Adobe AIR를 사용하여 비디오 재생 애플리케이션을 개발하십시오. 비디오 재생 애플리케이션을 개발한 후에는 이를 소비자에게 배포해야 합니다. Flash Player를 사용하여 애플리케이션을 개발하는 경우 조직의 웹 사이트에서 호스팅할 수 있습니다. Adobe® AIR®를 사용하여 애플리케이션을 개발하는 경우 소비자가 애플리케이션을 다운로드하여 컴퓨터에 설치할 수 있도록 AIR 애플리케이션 설치 프로그램을 게시하십시오.

Adobe Primetime DRM에서 사용할 사용자 정의 비디오 재생 애플리케이션을 개발하는 방법에 대한 자세한 내용은 ActionScript 3.0 개발자 가이드, [Adobe 비디오 기술 센터](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)및 [Open Source Media](https://www.adobe.com/devnet/video/)Framework의 &quot;비디오 작업&quot; 장을참조하십시오.