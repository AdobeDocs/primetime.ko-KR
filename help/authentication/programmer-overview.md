---
title: 프로그래머용 개요
description: 프로그래머용 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---


# 프로그래머용 개요 {#programmers-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#introduction}

이 개요는 웹 사이트 또는 애플리케이션에 Adobe® Pass를 통합할 컨텐츠 공급자(프로그래머)를 대상으로 합니다. Kickstart 및 Integration 안내서를 포함한 추가 설명서는 아래의 관련 정보 를 참조하십시오.

오늘날 시청자는 언제 어디서나 인터넷에 접속하여 보호된 콘텐츠에 대한 액세스를 Programmer로부터 직접 요청할 수 있습니다. 그들은 일회성 이벤트를 시청하고 싶거나, 여러분이 방송하고 있는 전체 텔레비전 시리즈의 시청권을 찾고 있을지도 모릅니다.

그러나 보호된 콘텐츠에 대한 액세스를 허용하기 전에 고객이 해당 콘텐츠를 볼 수 있는지 여부를 결정해야 합니다. MVPD(Multichannel Video Programming Distribution)를 구독하는 것이 있습니까? 그렇다면 이 구독에 프로그래밍이 포함됩니까?

프로그래머에게는 시청자의 자격을 결정하는 것이 항상 간단한 것은 아니다. MVPD는 해당 고객에 대한 식별 데이터 및 액세스 권한을 보유합니다.  보호된 컨텐츠에 액세스하려고 하는 뷰어가 각기 다른 시스템이 있는 다양한 MVPD에 가입하고 있으며, 보호된 컨텐츠에 대한 뷰어의 권리 결정을 빠르게 복잡해지고 기술적으로 어려운 상황이 될 수 있음을 쉽게 파악할 수 있습니다.

![](assets/user-ent-by-progr.png)

*그림: 프로그래머가 직접 결정한 사용자 자격*

TV에 대한 Adobe Primetime 인증을 통해 프로그래머와 MVPD 간에 이러한 자격 부여 거래를 안전하게 중개합니다. Adobe Primetime 인증을 사용하면 프로그래머가 유효한 고객에게 보호된 콘텐츠를 쉽고 빠르고 안전하게 제공할 수 있습니다.

![](assets/user-ent-mediatedby-authn.png)

*그림: Adobe Primetime 인증을 통해 조정되는 사용자 자격*

Adobe Primetime 인증은 참여하는 MVPD와의 교환에서 프록시 역할을 하므로 뷰어에 일관된 사이트 간 인터페이스를 표시할 수 있습니다. 또한 Adobe Primetime 인증을 사용하면 뷰어에게 SSO(Single Sign-On) 인증 및 인증을 제공할 수 있습니다. 참여하는 모든 서비스에 대해 인증 및 인증이 추적되므로 가입자는 자신의 시스템에서 첫 번째 인증 후 다시 로그인할 필요가 없습니다.

* **인증** - MVPD로 해당 사용자가 알려진 고객임을 확인하는 프로세스입니다.
* **인증** - MVPD로 인증된 사용자에게 지정된 리소스에 대한 유효한 구독이 있음을 확인하는 프로세스입니다.

### Adobe Primetime 인증 작동 방식 {#HowItWorks}

프로그래머의 컨텐츠 보기 애플리케이션은 Access Enabler 클라이언트 구성 요소 또는 Clientless API의 RESTful 웹 서비스(스마트 TV, 게임 콘솔, 셋톱 박스 등과 같은 웹이 아닌 장치의 경우)를 사용하여 Adobe Primetime 인증과 상호 작용합니다. Access Enabler는 사용자의 시스템에서 실행되며 모든 자격 부여 워크플로우를 용이하게 합니다.  Access Enabler 구성 요소는 고객이 사이트에 액세스하여 보호된 콘텐츠를 요청할 때 Adobe 시 호스팅 사이트에서 다운로드됩니다.  Adobe Primetime 인증 서버는 Clientless 솔루션에서 사용되는 RESTful 웹 서비스를 호스팅합니다.

Adobe Primetime 인증에서는 다음 작업에 사용할 프리미티브를 제공하면서 실제 자격 부여 워크플로우를 처리합니다.

* ID를 설정합니다. (프로그래머는 Adobe Primetime 인증 자격 흐름의 &quot;요청자&quot;입니다.)
* 특정 MVPD로 사용자를 인증합니다.  (MVPD는 Adobe Primetime 인증 자격 흐름의 &quot;ID 공급자&quot; 또는 &quot;IdP&quot;입니다.)
* 특정 리소스에 대해 MVPD를 가진 사용자에게 권한을 부여합니다.
* 사용자를 로그아웃합니다.

프로그래머는 다음을 수행하는 상위 수준 웹 페이지 또는 플레이어 애플리케이션을 담당합니다.

* 사용자 인터페이스 구현
* Access Enabler 또는 Clientless API 웹 서비스와 상호 작용함

Adobe Primetime 인증의 목표는 프로그래머와 MVPD가 자격 확인을 처리할 수 있도록 간단한 모듈식 방법을 만드는 것입니다.

## 토큰 이해 {#understanding-tokens}

Adobe Primetime 인증 자격 솔루션은 인증 및 인증 워크플로우가 성공적으로 완료될 때 생성된 특정 데이터 조각을 생성하는 데 중점을 둡니다. 이러한 데이터 조각을 토큰이라고 합니다. 토큰은 수명이 제한됩니다. 만료되면 인증 및 인증 워크플로우의 재시작을 통해 토큰을 다시 발급해야 합니다.

토큰에 대한 자세한 내용은 다음 섹션을 참조하십시오.

* [토큰 유형](#token-types)
* [토큰 저장소](#token-storage)
* [토큰 보안](#token-security)
* [토큰 공유](#token-sharing)

### 토큰 유형 {#token-types}

인증 및 인증 워크플로우 동안 세 가지 유형의 토큰이 발급됩니다. AuthN 및 AuthZ 토큰은 &quot;장기간&quot;이며 사용자의 보기 환경에 지속성을 제공합니다. 미디어 토큰은 스트림 리핑을 통해 사기를 방지하기 위한 업계 우수 사례를 지원하는 단기 토큰입니다. 프로그래머는 MVPD와의 계약에 따라 각 토큰 유형에 대한 TTL(time-to-live) 값을 지정합니다. 프로그래머는 사업과 고객에게 가장 적합한 TTL 값을 결정합니다.

* **AuthN 토큰** (&quot;오랫동안&quot;): 성공적으로 인증되면 Adobe Primetime 인증은 요청 장치와 GUID(Globally Unique Identifier)와 모두 연결된 AuthN 토큰을 만듭니다.
   * Adobe Primetime 인증은 AuthN 토큰을 Access Enabler로 전송하여 클라이언트 시스템에서 안전하게 캐시합니다.  AuthN 토큰이 있고 만료되지 않은 동안에는 Adobe Primetime 인증을 사용하는 모든 애플리케이션에서 사용할 수 있습니다. Access Enabler는 인증 흐름에 AuthN 토큰을 사용합니다.
   * 지정된 순간에 하나의 AuthN 토큰만 캐시됩니다. 새 AuthN 토큰이 발급되고 이전 토큰이 이미 있을 때마다 Adobe Primetime 인증이 캐시된 토큰을 덮어씁니다.
* **AuthZ 토큰** (&quot;오랫동안&quot;): 성공적으로 인증되면 Adobe Primetime 인증은 요청 장치 및 특정 보호된 리소스와 연결된 AuthZ 토큰을 만듭니다.  보호된 리소스는 고유한 리소스 ID로 식별됩니다.
   * Adobe Primetime 인증은 AuthZ 토큰을 Access Enabler로 전송하여 로컬 시스템에서 안전하게 캐시합니다. 그런 다음 Access Enabler는 AuthZ 토큰을 사용하여 실제 보기 액세스에 사용되는 단기 미디어 토큰을 만듭니다.
   * 지정된 시간에 리소스당 하나의 AuthZ 토큰만 캐시됩니다. Adobe Primetime 인증은 다른 리소스와 연결된 한 여러 AuthZ 토큰을 캐시할 수 있습니다. 새 AuthZ 토큰이 발급되고 동일한 리소스에 대해 이전 토큰이 이미 있을 때마다 Adobe Primetime 인증이 캐시된 토큰을 덮어씁니다.
* **미디어 토큰** (&quot;단기&quot;): Access Enabler는 AuthZ 토큰을 사용하여 단기(기본값: 7) 미디어 토큰. 성공적인 재생 요청이 발생한 것으로 간주되는 지점입니다.
   * 보호된 리소스에 대한 액세스를 제공하기 전에 미디어 서버가 미디어 토큰의 유효성을 검사하려면 Adobe Primetime 인증 구성 요소인 미디어 토큰 확인기를 사용해야 합니다.
   * 미디어 토큰이 장치에 바인딩되지 않으므로 지속 시간이 상당히 짧습니다(기본값: 7분)을 반환합니다.
   * 단기 미디어 토큰은 일회성 사용으로 제한되며 캐시되지 않습니다. 인증 API가 호출될 때마다 Adobe Primetime 인증 서버에서 검색됩니다.

### 토큰 저장소 {#token-storage}

Access Enabler는 해당 환경과 관련된 위치에 장기간 동안 토큰을 저장합니다(AuthN 및 AuthZ).

* **Flash 10.1** (이상): 긴 기간 토큰은 로컬 공유 개체로 저장됩니다.
* **HTML5**: 긴 기간 토큰은 HTML5 브라우저의 로컬 저장소에 안전하게 유지됩니다.
* **iOS**: 긴 기간 토큰은 다른 Adobe Primetime 인증 클라이언트 애플리케이션에서 액세스할 수 있는 영구 대지에 저장됩니다.
* **Android**: 긴 기간 토큰은 공유 데이터베이스 파일에 저장되어 다른 Adobe Primetime 인증 클라이언트 애플리케이션에서 액세스할 수 있습니다.
* **Clientless API 장치**: 토큰은 Primetime 인증 서버에 저장됩니다.

### 토큰 보안 {#token-security}

Adobe Primetime 인증 서버는 장치 ID(장치의 하드웨어 특성에서 파생됨)를 사용하여 긴 모든 토큰을 디지털 방식으로 서명합니다. 디지털 서명은 환경에 따라 생성, 보호 및 검증되는 방식에 따라 다릅니다.

* **Flash 10.1** (또는 이상) - 장치 ID는 Adobe 개인화 서버에서 발급한 고유 인증서인 장치 자격 증명을 사용합니다. 이 보안은 FAX DRM 기술과 같습니다. 이 서버측 유효성 확인은 토큰의 고유 장치 ID를 장치 자격 증명과 비교합니다(Flash Player에서 Adobe Primetime 인증과 안전하게 통신됨). 또한 장치 자격 증명은 FAX 클라이언트 버전과 발급된 Flash Player(또는 AIR) 버전을 식별합니다. 장치 바인딩은 HTML5보다 강력하므로 일반적으로 토큰의 TTL(time-to-live)은 Flash에서 더 깁니다.
* **HTML5** - 장치가 클라이언트 측에서 개별화되었습니다. JavaScript를 통해 사용할 수 있는 특성을 사용하여 브라우저 및 OS 버전, IP 주소 및 브라우저 쿠키 GUID(globally unique identifier)를 포함하는 의사 장치 ID를 생성합니다. 이 토큰 장치 ID는 장치의 현재 의사 장치 ID와 비교됩니다. IP 주소는 일반적인 사용 중에 변경될 수 있으므로 동일한 세션에서도 Adobe Primetime 인증은 HTML5 토큰을 두 위치에 저장합니다. localStorage 및 sessionStorage. IP가 변경되고 sessionStorage 토큰이 여전히 유효한 경우 세션이 유지됩니다. HTML5를 사용하면 장치 바인딩이 강력하지 않으므로 일반적으로 토큰에 대한 TTL이 Flash에 비해 짧습니다.
* **기본 클라이언트** (iOS 및 Android) - 장기 토큰은 기본 장치 ID 개인화 정보를 보유하므로 요청 장치에 바인딩됩니다. 인증 및 인증 요청은 HTTPS를 통해 전송되고, 장치 ID 정보는 Access Enabler 라이브러리에 의해 디지털 서명되어 백엔드 서버로 전송됩니다. 서버 측에서, 장치 ID 정보는 연결된 디지털 서명에 대해 확인됩니다.
* **Clientless API 클라이언트** - Clientless API 솔루션에는 모든 API 호출에 디지털 서명을 포함하는 보안 프로토콜 세트가 있습니다. 자격 흐름 중에 생성된 토큰은 Adobe Primetime 인증 서버에 안전하게 저장됩니다.

Adobe Primetime 인증은 긴 각 토큰을 확인하여 컨텐츠에 액세스하는 장치가 토큰을 발행한 토큰과 동일한지 확인합니다. 모든 토큰의 경우 클라이언트측 유효성 검사에서는 디지털 서명이 유지되고 토큰의 무결성이 보존됩니다. 장치 ID 유효성 검사가 실패하면 인증 세션이 무효화되고 사용자에게 다시 로그인하라는 메시지가 표시되어 토큰이 재설정됩니다.

### 토큰 공유 {#token-sharing}

다른 플랫폼의 애플리케이션은 토큰을 공유하지 않습니다. 다음과 같은 여러 가지 이유가 있습니다.

* 에 설명된 대로 [토큰 저장소](#token-storage), 토큰 저장 방법은 플랫폼(예: Flash을 위한 로컬 공유 개체, JavaScript용 웹 저장소)마다 다릅니다.
* 토큰 보안의 정도는 플랫폼마다 다릅니다. 예를 들어 Flash 토큰은 FXS를 사용하여 장치에 강력하게 바인딩됩니다. 순수 JavaScript 환경의 토큰은 Flash과 동일한 수준의 DRM 지원이 없습니다.  Flash 애플리케이션과 JS 토큰을 공유하면 더 안전한 환경을 사용하여 덜 안전한 토큰을 사용할 가능성이 높아집니다.

## 프로그래머 통합 라이프사이클 {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*그림: 프로그래머의 웹 사이트 및 애플리케이션과 인증 통합*


## 논리 흐름 {#logical-flows}

### 자격 순서도 {#chart}

다음 순서도는 Adobe Primetime 인증 Access Enabler 클라이언트 구성 요소를 사용하여 권한 확인을 수행하는 전체 프로세스를 보여 줍니다.

![](assets/ent-flowchart.png)

*그림: 자격 확인 프로세스*

### 인증 단계 {#authn-steps}

다음 단계에서는 Adobe Primetime 인증 흐름의 예를 보여줍니다.  프로그래머가 사용자가 MVPD의 유효한 고객인지 확인하는 자격 프로세스의 일부입니다.  이 시나리오에서는 사용자가 MVPD의 유효한 가입자입니다.  사용자가 Programmer의 Flash 응용 프로그램을 사용하여 보호된 콘텐츠를 보려고 합니다.

1. 사용자가 Programmer의 웹 페이지로 이동하여 Programmer의 Flash 응용 프로그램 및 Adobe Primetime 인증 Access Enabler 구성 요소를 사용자 시스템으로 로드합니다. Flash 응용 프로그램은 Access Enabler를 사용하여 Programmer의 ID를 Adobe Primetime 인증으로 설정하고 Adobe Primetime 인증은 Access Enabler를 해당 Programmer(&quot;요청자&quot;)의 구성 및 상태 데이터로 설정합니다. Access Enabler는 다른 API 호출을 수행하기 전에 서버에서 이 데이터를 수신해야 합니다. 기술 참고 사항: 프로그래머는 Access Enabler를 사용하여 ID 설정 `setRequestor()` 메서드 자세한 내용은 [Programmer Integration 안내서](/help/authentication/programmer-integration-guide-overview.md).
1. 사용자가 Programmer의 보호된 콘텐츠를 보려고 하면 Programmer의 응용 프로그램은 사용자가 공급자를 선택할 MVPD 목록을 사용자에게 표시합니다.
1. 사용자가 암호화된 Adobe Primetime 인증 서버로 리디렉션됩니다 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 사용자가 선택한 MVPD에 대한 요청이 만들어집니다. 이 요청은 프로그래머를 대신하여 MVPD에게 인증 요청으로 전송됩니다. MVPD 시스템에 따라 사용자의 브라우저는 MVPD 사이트로 리디렉션되어 로그인하거나 Programmer의 앱에서 로그인 iFrame을 만듭니다.
1. 어느 경우든(리디렉션 또는 iFrame) MVPD가 요청을 수락하고 로그인 페이지를 표시합니다.
1. 사용자가 MVPD로 로그인하고 MVPD가 유료 고객으로서의 사용자 상태를 확인한 다음 MVPD가 자체 HTTP 세션을 만듭니다.
1. 사용자의 유효성을 검사하면 MVPD는 MVPD가 Adobe Primetime 인증으로 다시 보내는 응답(SAML 및 암호화)을 만듭니다.
1. Adobe Primetime 인증은 MVPD 응답을 수신하고, Adobe Primetime 인증 HTTP 세션이 열려 있는지 확인하고, MVPD에서 SAML 응답을 확인한 다음, 프로그래머 사이트로 다시 리디렉션합니다.
1. Programmer의 사이트가 다시 로드되고 Access Enabler가 다시 로드되고 Programmer가 setRequestor()를 다시 호출합니다.  현재 구성이 변경되었기 때문에 setRequestor()에 대한 두 번째 호출이 필요합니다. 이제 Access Enabler에 서버에서 AuthN 토큰이 생성되기를 기다리고 있음을 알리는 플래그가 있습니다.
1. Access Enabler는 보류 중인 인증이 있음을 확인하고 Adobe Primetime 인증 서버에서 토큰을 요청합니다. 토큰은 Flash Player의 DRM 기능을 호출하여 서버에서 검색됩니다.
1. AuthN 토큰은 Programmer의 Flash Player LSO 캐시에 저장됩니다. 이제 인증이 완료되고 세션이 Adobe Primetime 인증 서버에서 제거됩니다.

### 인증 단계 {#authz-steps}

다음 단계는 [인증 단계](#authn-steps):

1. 사용자가 Programmer의 보호된 콘텐츠에 액세스하려고 하면 Programmer의 애플리케이션은 사용자의 로컬 시스템 또는 장치에서 AuthN 토큰을 먼저 확인합니다.  해당 토큰이 없으면 [인증 단계](#authn-steps) 위의 항목이 따릅니다.  AuthN 토큰이 있는 경우 권한 부여 플로우는 보호된 컨텐츠의 특정 항목에 대한 사용자의 보기 권한을 가져오도록 요청하여 Access Enabler에 대한 호출을 시작하는 Programmer의 응용 프로그램으로 진행됩니다.
1. 보호된 컨텐츠의 특정 항목은 &quot;리소스 식별자&quot;로 표시됩니다.  간단한 문자열이거나 더 복잡한 구조일 수 있지만, 어떤 경우든, Programmer와 MVPD 간에 미리 리소스 식별자의 특성에 대해 동의됩니다.  Programmer의 응용 프로그램은 리소스 식별자를 Access Enabler로 전달합니다.  Access Enabler는 사용자의 로컬 시스템 또는 장치에서 AuthZ 토큰을 확인합니다.  AuthZ 토큰이 없으면 Access Enabler가 요청을 백엔드 Adobe Primetime 인증 서버에 전달합니다.
1. Adobe Primetime 인증 서버는 표준화된 프로토콜을 사용하여 MVPD의 인증 종단점과 통신합니다.  MVPD의 응답에 보호된 콘텐츠를 볼 수 있는 권한이 사용자에게 있음을 나타내는 경우 Adobe Primetime 인증 서버는 AuthZ 토큰을 만들어 사용자 컴퓨터에 AuthZ 토큰을 저장하는 Access Enabler로 다시 전달합니다.
1. 사용자의 시스템 또는 장치에 저장된 AuthZ 토큰을 사용하여 Programmer의 애플리케이션은 Access Enabler를 호출하여 Adobe Primetime 인증 서버에서 미디어 토큰을 가져오고 해당 토큰을 Programmer의 애플리케이션에 제공합니다.
1. 마지막으로, Programmer의 응용 프로그램은 미디어 토큰 확인기 구성 요소를 사용하여 올바른 사용자가 올바른 컨텐츠를 보고 있는지 확인하고, 미디어 토큰을 제자리에 두고 사용자는 보호된 콘텐츠를 볼 수 있습니다.


## 등록 및 초기화 {#reg-and-init}

Adobe Primetime 인증을 사용하는 첫 번째 단계는 Adobe 또는 Adobe Primetime 인증 파트너에 등록하는 것입니다.

등록할 때 Adobe Primetime 인증과 통신할 도메인의 목록을 제공합니다. 예를 들어 Turner Broadcast System 도메인은 tbs.com 및 tnt.tv 를 Adobe Primetime 인증 등록 도메인으로 포함합니다. 이러한 각 컨텐츠 사이트에는 Adobe Primetime 인증에 액세스할 수 있고, 고유한 요청자 ID(예: &quot;TBS&quot; 및 &quot;TNT&quot;)가 할당됩니다. 추가 사이트를 추가하기로 결정한 경우 Adobe에게 추가 도메인 이름을 알려서 허용 도메인 목록에 추가하고 추가 요청자 ID를 제공해야 합니다.

>[!WARNING]
>
>통합을 테스트하는 동안 테스트 서버가 프로덕션에 사용할 등록된 도메인에 있는지 확인하십시오. 화이트리스트에 포함되지 않은 도메인에서 오는 요청, 테스트 요청도 무시됩니다. 예를 들어, 프로덕션 환경에서 domain.com을 사용하도록 요청한 경우, domain.com, test.domain.com 및 staging.domain.com 아래에 테스트 통합을 배포하고 있는지 확인하십시오.
>
>도메인을 화이트리스트에 추가하더라도 URL에 사용자 이름 및 / 또는 암호가 포함된 요청은 무시됩니다. 예: `//username@registered-domain/`

요청자 ID는 Adobe Primetime 인증의 Access Enabler 클라이언트 구성 요소와 모든 통신에서 프로그래머의 클라이언트를 고유하게 식별합니다. 프로그래머와 연결된 모든 Adobe Primetime 인증 정적 데이터는 이 ID를 사용합니다.

>[!TIP]
>
>요청자 ID 외에도 등록 시 Access Enabler 클라이언트 구성 요소와 미디어 토큰 확인기의 기능 URL도 받게 됩니다.

## 통합 단계 {#integration-steps}

>[!TIP]
>
>미디어 플레이어 개발에 Adobe의 Open Source Media Framework(&quot;OSMF&quot;)를 사용하는 경우 Adobe Primetime 인증을 사용하는 가장 빠른 방법은 OSMF 플러그인을 통합하는 것입니다 *(더 이상 사용되지 않음)* 플레이어의 코드에 연결합니다.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [요청자 설정](#requestor)
1. [인증 및 인증 처리](#authn-authz)
1. [단일 로그아웃 지원](#ssl)

### 1. 요청자 설정 {#requestor}

#### 1a. Adobe에 등록

첫 번째 단계는 Adobe 또는 Adobe Primetime 인증 인증 파트너에 등록하는 것입니다.  등록할 때 하나 이상의 GUID(Globally Unique Identifier)가 발급됩니다. 발급된 각 GUID는 Adobe Primetime 인증에 액세스할 수 있는 도메인에 연결됩니다. 요청 도메인에 대해 요청자 ID라고 하는 GUID를 전달하여 Access Enabler와 상호 작용하는 각 세션에 대한 ID를 등록합니다. 자세한 내용은 [등록 및 초기화](#reg-and-init) 을 참조하십시오.

#### 1b. 초기 액세스 Enabler 통합

다음 단계는 기존 미디어 플레이어 앱 또는 웹 페이지에 Access Enabler를 통합하는 것입니다.

* Flash 버전을 포함할 수 있습니다. `AccessEnabler.swf`를 포함할 수도 있습니다. ActionScript 또는 JavaScript에서 Access Enabler SWF과 통신할 수 있습니다. 기본 API는 ActionScript이지만 JavaScript를 사용하려는 경우 페이지에 포함할 수 있는 전체 래퍼 라이브러리를 사용할 수 있습니다.
* Flash이 아닌 환경의 경우 다음을 수행할 수 있습니다.
   * HTML5/JavaScript 버전, AccessEnabler.js를 사용하고 JavaScript API를 통해 통신합니다
   * Adobe Primetime 인증을 위한 AIR Native Extension을 사용하여 기본 코드와 내장 ActionScript 클래스를 결합합니다.
   * Access Enabler 라이브러리의 기본 클라이언트 버전 중 하나를 사용합니다(iOS 또는 Android)

### 2. 인증 및 인가의 처리 {#authn-authz}

#### 2a. Access Enabler와 통신

Access Enabler와 웹 페이지 또는 플레이어 앱 간의 통신은 비동기적으로 수행됩니다. 애플리케이션이 Access Enabler 메서드를 호출하고 Access Enabler 라이브러리에 등록하는 콜백을 통해 Access Enabler가 응답합니다.

* 응용 프로그램에서 인증 요청을 수행하면 유효한 AuthN 토큰이 로컬 시스템에 없는 경우 Access Enabler가 자동으로 인증 요청을 시작합니다. 인증이 성공하면 사용자의 AuthN 토큰이 로컬로 저장되므로 다시 로그인할 필요가 없습니다. 다른 컨텍스트(예: MVPD 웹 사이트 또는 다른 프로그래머를 통해)에서 Adobe Primetime 인증을 통해 인증되면 Access Enabler는 로컬 AuthN 토큰에 액세스할 수 있으며 추가 인증이 필요하지 않습니다.
* 사용자가 보호된 컨텐츠에 액세스하려고 하면 Access Enabler에 인증 요청을 보냅니다. 인증을 확인(또는 시작)한 후 Access Enabler는 Adobe Primetime 인증 서버를 통해 MVPD에 연락하여 고객이 보호된 콘텐츠를 볼 수 있는지 여부를 확인합니다. 애플리케이션이 Access Enabler에 요청을 보낸 다음 응답(인증 성공 또는 실패)을 처리해야 합니다. 인증이 성공하면 AuthZ 토큰이 클라이언트 시스템에 저장됩니다.  마지막으로, 애플리케이션은 자체 인증 절차에서 사용할 단기 미디어 토큰을 수신합니다.

>[!NOTE]
>
>* 인증은 SAML 교환으로서, SP(서비스 공급자)로 Adobe Primetime 인증과 MVPD를 ID 공급자(IdP)로 함 간에 발생합니다.
>
>* 권한 부여에서는 SP(Adobe Primetime 인증)와 MVPD(IdP) 간에 백 채널(서버 간) 웹 서비스 교환을 사용합니다.



#### 2 b. 자격 사용자 인터페이스 제공 {#entitlement-ui}

사용자가 컨텐츠에 액세스할 수 있도록 고유한 UI를 제공합니다. 실제 로그인 프로세스와 같은 일부 요소는 MVPD에서 제공하며, 일부 요소는 선택적으로 Adobe Primetime 인증의 일부로 사용할 수 있습니다. 최소한 다음을 수행합니다.

* **새 사용자가 MVPD를 식별하고 처음 로그인할 수 있도록 해주는 MVPD 선택 인터페이스를 구현합니다**. 개발을 위해 Access Enabler는 MVPD를 선택하고 로그인 프로세스를 시작하는 기본 사용자 인터페이스를 제공합니다. 프로덕션의 경우 자체 MVPD 선택기 대화 상자를 구현해야 합니다. 일부 MVPD는 로그인을 위해 자신의 사이트로 리디렉션되며, 일부는 iFrame 내에 로그인 페이지를 표시해야 합니다. 사용자의 MVPD가 iFrame에 로그인 페이지를 표시하는 경우를 처리하려면 이 iFrame을 만드는 콜백을 구현해야 합니다.
* **보호된 콘텐츠 식별**. 보호된 콘텐츠에 액세스하려면 액세스 권한이 필요합니다. 인터페이스에서는 어떤 컨텐츠가 보호되고 어떤 컨텐츠가 인증되었는지 표시해야 합니다.  인증 상태는 종종 &quot;잠금 해제&quot; 및 &quot;잠금&quot; 아이콘으로 표시됩니다.
* **사용자가 인증되었음을 표시합니다.**. 보호된 콘텐츠를 식별하는 데 사용하는 수단의 일부로 사용자의 인증 상태를 표시해야 합니다. Access Enabler를 쿼리하여 고객이 이미 인증되었는지 확인할 수 있습니다.

#### 2c. 미디어 토큰 확인 프로그램 통합 {#int-media-token-ver}

Adobe Primetime 인증 미디어 토큰 확인 프로그램 구성 요소를 미디어 서버에 통합해야 합니다.  이렇게 하면 기존 토큰 확인기가 성공적으로 인증되어 Adobe Primetime 인증에서 제공된 단기 미디어 토큰을 인식할 수 있습니다. 미디어 토큰 확인기는 사용자가 보호된 콘텐츠에 액세스할 수 있도록 하기 전에 마지막 보안 단계로 미디어 토큰의 유효성을 검사합니다. Adobe에 등록할 때 미디어 토큰 확인기를 다운로드할 위치를 받습니다.

### 3. 단일 로그아웃 지원 {#ssl}

대부분의 경우 미디어 플레이어는 간단한 Access Enabler API를 통해 사용자 로그아웃을 처리합니다. logout()를 호출하면 Access Enabler가 다음을 수행합니다.

* 현재 사용자를 로그아웃합니다
* 로그아웃 사용자에 대한 모든 인증 및 인증 정보를 지웁니다
* 사용자의 로컬 시스템에서 모든 AuthN 및 AuthZ 토큰을 삭제합니다

사용자가 토큰이 만료될 때까지 시스템 유휴 상태를 충분히 오래 두면 사용자는 여전히 세션으로 돌아가서 성공적으로 로그아웃할 수 있습니다. Adobe Primetime 인증을 사용하면 모든 토큰이 삭제되고 MVPD에게 세션도 삭제하도록 알립니다.

Adobe Primetime 인증과 통합되지 않은 사이트에서 로그아웃을 시작하면 MVPD는 브라우저 리디렉션을 통해 Adobe Primetime 인증 단일 로그아웃 서비스를 호출할 수 있습니다.

## 사용자 ID 이해 {#user-ids}

개념적으로, 자격 흐름을 시작하는 각 사용자는 하나의 고유한 사용자 ID와 연결됩니다.  그러나 자격 흐름 과정을 통해 ID를 얻는 API에 따라 하나의 사용자 ID를 다른 방식으로 제공할 수 있습니다.

Short Media 토큰의 sessionGUID는 sendTrackingData() 호출을 통해 사용할 수 있는 UserID의 보안 형식입니다.   모든 현재 통합에서 시간 및 장치에서 사용자에 대한 영구 GUID지만 GUID의 소스는 MVPD의 SAML 응답에서 UserID로 시작합니다.   그러나 일부 MVPD는 나중에 생각이 바뀔 수 있으며 임시 GUID를 보내기 시작할 수 있습니다.  프로그래머가 AuthN 응답의 MVPD 소스 UserID가 영구적인지 확인하려는 경우 MVPD와의 계약에 이를 배치해야 합니다.

사용자 ID가 Adobe Primetime 인증 API에 표시되는 방법은 다음과 같습니다.

* `sendTrackingData()` GUID 속성 - MVPD UserID의 Adobe 해시된 버전입니다.  해시되므로 이 사용자 ID가 MVPD의 소스로 다시 추적할 수 없습니다.   이 ID는 고유하며 일반적으로 영구적이지만, 특정 사용 행동을 MVPD가 속한 사용과 비교하기 위해 MVPD와 공유할 수 없습니다.   디지털 서명이 아니므로 사기 방지를 위해 스푸핑할 수 없지만 분석에는 충분합니다.  이 사용자 ID 형식은 Adobe Primetime 인증이 AuthN/AuthZ 플로우에서 생성하는 모든 이벤트에 대해 클라이언트측에서 제공됩니다.
* 짧은 미디어 토큰 `sessionGUID` 속성 - 를 통해 UserID와 동일합니다 `sendTrackingData()`그러나 이 디지털 서명을 통해 무결성을 보호합니다.  이렇게 하면 동시 사용의 부정 추적 시 이 값이 충분히 향상됩니다. 유효성 검사기 라이브러리를 사용한 후에 서버 측에서 처리되도록 작성되었으며, 비디오 스트림을 클라이언트에 릴리스하기 전에 사기 패턴을 분석할 수 있습니다.  이런 일을 하는 것은 프로그래머에게 달려 있다.
* `getMetadata() userID `속성 - 이 속성을 사용하면 Adobe이 실제 소스 MVPD UserID를 Programmer에 노출할 수 있습니다. 이 정보는 Programmer에서 받은 인증서의 공개 키로 암호화되므로 클라이언트로 명확하게 노출되지 않습니다. 이를 통해 프로그래머에게 MVPD의 실제 UserID를 제공하므로 MVPD와 직접 계정 연결 또는 사기 조사에 사용할 수 있습니다.

**결론적으로**

* MVPD 사용자 ID는 일반적으로 보장되지 않지만 다음 고유한 ID인 영구 고유 ID입니다 **mvpd에서 생성되어 인증 성공 시 Adobe에 전달됨**. 일반적으로 일부 예외가 있는 모든 네트워크에서 일관됩니다.
* MVPD 사용자 ID에 PII가 포함되어 있지 않으며 계정 번호가 아닙니다. PII가 전송되지 않는 모든 MVPD를 사용하여 유효성 검사를 수행했으므로 암호화된 양식으로 노출될 필요가 없습니다.


사용자 ID 사용 방법은 사용 사례에 따라 다릅니다.

* 추적/분석을 위해 필요한 경우 가장 실용적인 장소는 를 가져오는 것입니다. `sendTrackingData()`.
* 스트림 릴리스, 사기 또는 운영 데이터에 대해 서버측에서 필요한 경우 Media Token Validator에서 가져올 수 있습니다.
* 계정 연결 및 더 심층적인 사기를 위해 필요한 경우 Adobe 담당자에게 문의하십시오.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->