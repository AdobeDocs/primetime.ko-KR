---
description: Adobe Access의 기본 구성 요소는 Java SDK, Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.
seo-description: Adobe Access의 기본 구성 요소는 Java SDK, Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.
seo-title: Java SDK, Flash Player 및 Adobe AIR 클라이언트
title: Java SDK, Flash Player 및 Adobe AIR 클라이언트
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Adobe Access 구성 요소{#adobe-access-components}

Adobe Access의 기본 구성 요소는 Java SDK, Flash Player 및 Adobe AIR 클라이언트 런타임 환경으로 구성됩니다.

SDK 설정에 대한 자세한 내용은 컨텐츠 보호를 위한 Adobe Access SDK *사용의 SDK 설정을 참조하십시오.*

Adobe Access SDK를 사용하면 콘텐츠 관리, 청구 및 사용자 액세스 제어 시스템 등 조직의 기존 비즈니스 인프라와 통합되는 디지털 권한 관리 솔루션을 개발할 수 있습니다. Flash Player와 Adobe AIR를 사용하면 소비자가 대규모 디지털 컨텐츠 라이브러리를 이용하고 볼 수 있는 애플리케이션을 제작하고 손쉽게 배포할 수 있습니다.

## Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access는 서버 구현을 만들 수 있는 빌드 블록을 제공하는 Java SDK로 제공됩니다. SDK를 사용하면 조직의 비즈니스 모델에 적합한 Adobe Access 솔루션을 만들 수 있습니다.

SDK에 제공된 Java API는 다음 하위 섹션에 설명되어 있습니다.

## 장치 그룹 도메인 관리를 위한 Java API {#java-apis-for-managing-device-group-domains}

이 API는 서버가 장치 그룹 도메인 연결 및 종료에 대한 클라이언트 요청을 처리할 수 있도록 하는 데 사용됩니다.

장치 그룹 도메인은 서로 라이센스를 공유할 수 있는 장치의 논리적 모음입니다. 이렇게 하려면 각 장치가 먼저 동일한 도메인에 가입하거나 등록해야 합니다. 서버에서 실행 중인 Adobe Access SDK는 장치 도메인 가입(등록) 요청뿐만 아니라 장치 도메인 임대(등록 취소) 요청도 처리해야 합니다. 도메인에 가입되지 않은 장치는 해당 장치에 바인딩되어 다른 장치에 공유할 수 없는 라이센스를 발급하게 됩니다.

## 컨텐츠 보호를 위한 Java API {#java-apis-for-protecting-content}

이러한 API 파섹 컨텐츠 보호 API는 다음과 같습니다.

* 정책 관리

   정책 관리 API 파섹 모든 사용 규칙을 가져오거나 설정하고 사용자 지정 네임스페이스에 추가 매개 변수를 허용하는 등 정책을 만들거나 업데이트할 수 있습니다.

* 컨텐츠 패키징

   콘텐츠 패키징 API는 콘텐츠를 암호화하고 패키지된 콘텐츠에서 메타데이터를 가져오는 데 사용됩니다.

## 라이선스 발급을 위한 Java API {#java-apis-for-issuing-licenses}

이러한 API는 클라이언트가 서버에서 라이센스를 요청할 때 사용됩니다. SDK는 클라이언트의 다음 요청을 지원합니다.

* 인증

   인증 API를 사용하여 인증 요청을 처리하고 인증 토큰을 생성할 수 있습니다.

* 라이선스 생성 및 확보

   라이선스 생성 및 획득 API는 사용자의 라이센스를 생성하는 데 사용됩니다.

* Adobe AIR 버전 1.5 클라이언트 및 컨텐츠 지원

   이전 버전과의 호환성을 위해 SDK에는 AIR 버전 1.5 이전 클라이언트 및 보호된 컨텐츠와 함께 사용하기 위해 만들어진 AIR 애플리케이션의 요청을 처리할 수 있는 API가 있습니다.

## 참조 구현 {#reference-implementation}

SDK에는 Java API를 사용하는 방법을 설명하는 간단한 Adobe Access 배포인 참조 구현이 포함되어 있습니다. 참조 구현은 Java API를 기반으로 하는 컨텐츠 패키징 및 정책 관리를 위한 명령줄 툴, 라이선스 서버, 감시 폴더 패키저, Adobe Access Manager AIR 애플리케이션을 제공합니다. Adobe Access 참조 구현에 대한 자세한 내용은 컨텐츠 보호를 *참조하십시오*.

## 안전한 스트리밍을 위한 Adobe Access Server {#adobe-access-server-for-protected-streaming}

Adobe HTTP Dynamic Streaming과 같은 Adobe Access로 콘텐트를 보호하는 스트리밍 사용 사례를 위해 이 소프트웨어에는 안전한 스트리밍을 위한 Adobe Access Server도 포함되어 있습니다. 이 솔루션은 Tomcat과 같은 서블릿 컨테이너에 쉽게 배포할 수 있으며 대규모 컨텐츠 배포 요구 사항을 충족하기 위해 높은 수준의 확장성 및 성능을 얻을 수 있습니다.

## Adobe Flash Player {#adobe-flash-player}

Flash Player는 크기가 작은 브라우저 플러그인과 런타임으로, 일관되고 매력적인 사용자 경험, 시선을 사로잡는 오디오/비디오 재생 및 광범위한 전달 범위를 제공합니다. Flash Player는 스트리밍되거나 다운로드된 비디오 컨텐츠를 고품질의 재생으로 제공합니다. 컨텐츠 퍼블리셔의 경우 Flash Player는 컨텐츠 주위의 재생 화면을 사용자 정의할 수 있는 방법을 제공하므로 배너와 오버레이를 사용한 광고를 통해 보다 심층적인 브랜딩 경험과 상용화를 경험할 수 있습니다. 소비자의 경우 Flash Player는 직관적이고 시각적으로 비디오 컨텐츠를 볼 수 있는 방법을 제공합니다.

Flash Player에 대한 자세한 내용은 다음을 참조하십시오. [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR는 크로스 운영 체제 런타임으로 컨텐츠 제작자는 맞춤형 멀티미디어 애플리케이션을 디자인하여 웹에 대한 기존 투자를 데스크탑으로 확대할 수 있습니다. 업계에서 입증된 개방형 기술을 기반으로 구축되어 안정적이고 간소화된 방식으로 신뢰할 수 있는 맞춤형 애플리케이션을 개발 및 배포하여 보다 안전하고 매력적인 사용자 경험을 제공할 수 있습니다. 기업은 Adobe AIR를 통해 리치 미디어를 손쉽게 통합하여 보다 매력적이고 인터랙티브한 사용자 경험을 제작할 수 있습니다. 개발자는 HTML, JavaScript, Flash 또는 Adobe® Flex® 소프트웨어와 같은 익숙한 툴을 사용하여 리치 인터넷 애플리케이션의 고유한 조합을 Windows, Macintosh 또는 Linux에 배포할 수 있습니다.

기업은 유저 인터페이스를 완벽하게 제어할 수 있으며 자사 브랜드를 반영하고 강화하기 위해 사용자 경험을 디자인할 수 있습니다. Adobe Access SDK로 보호되는 컨텐츠 재생을 위한 내장된 지원을 제공하는 Adobe AIR를 사용하면 완벽한 맞춤형 컨텐츠 배포 체인을 만들 수 있습니다.

Adobe AIR에 대한 자세한 내용은 다음을 참조하십시오. [www.adobe.com/go/air](https://www.adobe.com/go/air)

## 기본 iOS 및 Android 애플리케이션 {#native-ios-and-android-applications}

Adobe Primetime 고객에게만 제공되는 기본 iOS 및 Android 애플리케이션 Adobe Access DRM 4.0 이상은 모바일 디바이스의 기본(Flash가 아닌) 애플리케이션에서 사용되는 비디오를 보호하는 데 사용할 수 있습니다. 응용 프로그램이 이 보호된 콘텐츠를 사용하려면 Adobe Primetime 클라이언트 라이브러리를 사용하여 구현해야 합니다.

Adobe Primetime에 대한 자세한 내용은 다음을 참조하십시오. [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)