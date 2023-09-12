---
description: Adobe 액세스의 주요 구성 요소는 Java SDK와 Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.
title: Java SDK, Flash Player 및 Adobe AIR 클라이언트
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
source-git-commit: 8d7a4f69a6400b0c3242d4cb0c5daac81f27db3a
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Adobe 액세스 구성 요소{#adobe-access-components}

Adobe 액세스의 주요 구성 요소는 Java SDK와 Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.

SDK 설정에 대한 자세한 내용은 다음에서 SDK 설정 을 참조하십시오. *컨텐츠 보호를 위해 Adobe 액세스 SDK 사용.*

Adobe 액세스 SDK를 사용하면 콘텐츠 관리, 청구 및 사용자 액세스 제어 시스템과 같은 조직의 기존 비즈니스 인프라와 통합하는 디지털 권한 관리 솔루션을 개발할 수 있습니다. Flash Player 및 Adobe AIR을 사용하면 소비자가 디지털 컨텐츠의 대용량 라이브러리에 액세스하고 볼 수 있도록 애플리케이션을 만들고 쉽게 배포할 수 있습니다.

## Adobe 액세스 SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe 액세스는 서버 구현을 만들 수 있는 기본 구성 요소를 제공하는 Java SDK로 제공됩니다. SDK를 사용하여 조직의 비즈니스 모델에 맞는 Adobe 액세스 솔루션을 만들 수 있습니다.

SDK에 제공된 Java API는 다음 하위 섹션에 설명되어 있습니다.

## 장치 그룹 도메인 관리를 위한 Java API {#java-apis-for-managing-device-group-domains}

이러한 API는 서버가 장치 그룹 도메인에 가입하고 나가는 클라이언트 요청을 처리할 수 있도록 하는 데 사용됩니다.

장치 그룹 도메인은 서로 라이선스를 공유할 수 있는 장치의 논리적 컬렉션입니다. 이렇게 하려면 각 디바이스가 먼저 동일한 도메인에 가입/등록해야 합니다. 서버에서 실행 중인 Adobe 액세스 SDK는 장치 도메인 가입(등록) 요청과 장치 도메인 탈퇴(등록 취소) 요청을 처리해야 합니다. 도메인에 가입되지 않은 장치에는 해당 장치에 바인딩된 라이선스가 발급되며, 이 라이선스는 다른 장치와 공유할 수 없습니다.

## 콘텐츠 보호를 위한 Java API {#java-apis-for-protecting-content}

이러한 API는 권한을 정의하고 배포할 콘텐츠를 준비하는 데 사용됩니다. 콘텐츠 보호 API는 다음과 같습니다.

* 정책 관리

  정책 관리 API는 콘텐츠에 적용할 정책을 만들고 수정하는 데 사용됩니다. 모든 사용 규칙을 가져오거나 설정하고, 사용자 지정 네임스페이스에서 추가 매개 변수를 허용하는 등 정책을 만들거나 업데이트할 수 있습니다.

* 컨텐츠 패키징

  컨텐츠 패키징 API는 컨텐츠를 암호화하고 패키징된 컨텐츠에서 메타데이터를 검색하는 데 사용됩니다.

## 라이선스 발급을 위한 Java API {#java-apis-for-issuing-licenses}

이러한 API는 클라이언트가 서버에서 라이선스를 요청할 때 사용됩니다. SDK는 클라이언트의 다음 요청을 지원합니다.

* 인증

  인증 API를 사용하여 인증 요청을 처리하고 인증 토큰을 생성할 수 있습니다.

* 라이선스 생성 및 획득

  라이선스 생성 및 획득 API는 사용자를 위한 라이선스를 생성하는 데 사용됩니다.

* Adobe AIR 버전 1.5 클라이언트 및 콘텐츠 지원

  이전 버전과의 호환성을 위해 SDK에는 AIR 버전 1.5 및 이전 버전의 클라이언트와 보호된 콘텐츠에서 사용하기 위해 만들어진 AIR 애플리케이션의 요청을 처리하는 API가 있습니다.

## 참조 구현 {#reference-implementation}

SDK에는 Java API를 사용하는 방법을 보여 주는 간단한 Adobe 액세스 배포인 참조 구현이 포함되어 있습니다. 참조 구현은 Java API를 기반으로 하는 콘텐츠 패키징 및 정책 관리를 위한 라이선스 서버, 감시 폴더 패키지, Adobe 액세스 관리자 AIR 애플리케이션 및 명령줄 도구를 제공합니다. Adobe 액세스 참조 구현에 대한 자세한 내용은 다음을 참조하십시오. *콘텐츠 보호*.

## Adobe Access Server for Protected Streaming {#adobe-access-server-for-protected-streaming}

Adobe HTTP Dynamic Streaming과 같이 콘텐츠가 Adobe 액세스로 보호되는 스트리밍 사용 사례의 경우, 소프트웨어에는 보호되는 스트리밍용 Adobe Access Server 도 포함됩니다. 이 솔루션은 Tomcat과 같은 서블릿 컨테이너에 쉽게 배포할 수 있으며 가장 큰 컨텐츠 배포 요구 사항을 충족하는 높은 수준의 확장성과 성능을 구현할 수 있습니다.

## Adobe Flash Player {#adobe-flash-player}

Flash Player은 일관되고 매력적인 사용자 경험, 놀라운 오디오/비디오 재생 및 광범위한 도달 범위를 제공하는 간단한 브라우저 플러그인 및 런타임입니다. Flash Player은 스트리밍되거나 다운로드된 비디오 컨텐츠를 고품질로 재생합니다. 컨텐츠 게시자의 경우, Flash Player은 컨텐츠를 둘러싼 재생 화면을 사용자 정의할 수 있는 수단을 제공하여 배너 및 오버레이를 사용한 광고를 통해 더 깊은 브랜딩 경험과 수익을 얻을 수 있습니다. 소비자를 위해 Flash Player은 비디오 컨텐츠를 볼 수 있는 직관적이고 시각적으로 호소력 있는 방법을 제공합니다.

Flash Player에 대한 자세한 내용은 다음을 참조하십시오. [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR은 맞춤형 멀티미디어 애플리케이션을 설계하여 콘텐츠 제작자가 웹에 대한 기존 투자를 데스크톱까지 확장할 수 있는 크로스 운영 체제 런타임입니다. 검증된 개방형 기술을 기반으로 구축된 이 솔루션은 신뢰할 수 있는 맞춤형 애플리케이션을 개발 및 배포하여 보다 안전하고 즐거운 사용자 경험을 제공할 수 있도록 안정적이고 단순화된 방법을 제공합니다. Adobe AIR을 통해 기업은 리치 미디어를 손쉽게 통합하여 보다 몰입적이고 인터랙티브한 사용자 경험을 만들 수 있습니다. 개발자는 HTML, JavaScript, Flash 또는 Adobe® Flex® 소프트웨어와 같은 친숙한 도구를 사용하여 풍부한 인터넷 응용 프로그램의 고유한 조합을 Windows, Macintosh 또는 Linux에 배포할 수 있습니다.

기업은 사용자 인터페이스를 완벽하게 제어할 수 있으며 사용자 경험을 설계하여 브랜드를 반영하고 강화할 수 있습니다. Adobe AIR은 Adobe 액세스 SDK로 보호된 콘텐츠의 재생을 기본적으로 지원하므로 사용자 지정 종단간 콘텐츠 배포 체인을 만들 수 있습니다.

## 기본 iOS 및 Android 애플리케이션 {#native-ios-and-android-applications}

네이티브 iOS 및 Android 애플리케이션 Adobe Primetime 고객만 사용할 수 있는 Adobe 액세스 DRM 4.0 이상을 사용하여 모바일 장치의 네이티브(Flash이 아닌) 애플리케이션 내에서 사용되는 비디오를 보호할 수 있습니다. 애플리케이션이 이 보호된 콘텐츠를 사용하려면 Adobe Primetime 클라이언트 라이브러리를 사용하여 구현해야 합니다.

Adobe Primetime에 대한 자세한 내용은 다음을 참조하십시오. [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
