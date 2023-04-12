---
title: MVPD 개요
description: MVPD 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# MVPD에 대한 개요 {#mvpd-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#intro}

이 개요는 MVPD(다중 채널 비디오 프로그래밍 배포)를 위한 것입니다. Kickstart 및 Integration Guides를 포함한 추가 설명서는 이 문서의 끝에 있는 Related Information 섹션을 참조하십시오.



TV Everywhere(TVE)는 이제 잘 알려진 업계 운동으로, 유료 TV 가입자들이 집 안팎에서, 여러 장치들에서, 이미 지불한 콘텐츠에 액세스할 수 있도록 합니다.  유료 TV 제공업체에게 TVE는 기존 고객 관계를 유지하고 새로운 고객을 가능하게 하는 새로운 기회를 창출합니다. 그러나 이러한 기회들과 함께 도전들이 옵니다. TVE 가로에서는 프로그래머가 컨텐츠를 제공하지만 MVPD는 예상 뷰어가 유효한 구독자인지 확인하기 위한 고객 정보를 보유합니다.



한 프로그래머와 뷰어 인증을 조정하고 승인을 조정하는 것은 간단할 수 있지만 수십 또는 수백 명의 프로그래머와 조정하는 것은 점점 복잡해지고 있습니다. 그러나 Adobe® Pass를 사용하는 MVPD는 NBCUnversal Media, Turner Broadcast(TBS, TNT, CNN), Fox Broadcast Networks, Hulu 등과 같은 전체 TVE 에코시스템에 액세스할 수 있도록 단일 통합 구현만 하면 됩니다.  Adobe Primetime 인증은 사용자 권한을 간단하고 안전하게 결정하는 통합 프레임워크를 제공합니다.



최종본: Adobe Primetime 인증은 프로그래머와 MVPD 간의 자격 트랜잭션을 안전하게 조정하므로 뷰어가 구독 컨텐츠에 쉽게 액세스할 수 있습니다. 즉, Adobe Primetime 인증을 통해 적합한 고객이 적합한 콘텐츠를 쉽고 빠르게 액세스할 수 있습니다.


Adobe Primetime 인증을 통해 MVPD는 다음을 받습니다.

프로그래머와 손쉽게 통합  단일 통합을 통해 여러 컨텐츠 소유자로부터 즉각적인 연결을 제공합니다.

고객 참여 개선.  고객이 여러 플랫폼 및 장치에서 콘텐츠를 볼 때 매끄러운 브랜드 경험을 지원합니다.

보안 인증.  권한이 있는 사용자 및 장치만 프리미엄 컨텐츠에 액세스할 수 있도록 하고, (선택적으로) 가구 계정별로 연결할 수 있는 장치 및 동시 스트림 수를 제한하십시오.

## FAQ {#faq}

Adobe Primetime 인증의 보안 방식 Adobe Primetime 인증 아키텍처의 최우선 과제는 인증된 뷰어만 인증되고 프리미엄 컨텐츠에 대한 액세스 권한이 부여되도록 하는 것입니다. Adobe Primetime 인증은 보기 장치에 대한 액세스를 긴밀하게 결합하며, 특정 가구에 대한 스트림, 세션 및/또는 장치를 제한하는 데 도움이 될 수 있습니다.


Flash Player이 필요합니까? TV Everywhere용 Adobe Primetime 인증은 플레이어 및 플랫폼에 영향을 받지 않으며 Silverlight 및 HTML5를 비롯한 모든 재생 애플리케이션과 통합됩니다. 또한 Adobe Primetime 인증은 iOS 및 Android를 실행하는 휴대폰 및 태블릿과 같은 장치에 대한 기본 지원을 제공합니다.


Adobe Primetime 인증이 지원하는 장치는 무엇입니까? Adobe Primetime 인증은 브라우저 내 보기 환경을 위한 HTML5 웹 키트를 사용하는 거의 모든 장치에서 지원됩니다. 또한 Adobe Primetime 인증에서는 iOS, Android™, Xbox360(더 이상 사용되지 않음) 및 Campaign Air®(더 이상 사용되지 않음) 애플리케이션을 포함하여 다양한 장치 특정 플랫폼에 대한 기본 소프트웨어 개발 키트(SDK)를 계속 롤아웃합니다. 가장 최근, Adobe Primetime 인증은 브라우저 페이지를 렌더링할 수 없는 장치(예: &quot;스마트&quot; TV, 셋톱 박스 및 게임 콘솔)에 대해 클라이언트 없는 솔루션을 출력합니다.  브라우저 페이지를 렌더링하는 기능은 MVPD를 사용하여 사용자를 인증하는 요구 사항입니다.


Adobe Primetime 인증이 TV Everywhere의 최신 표준을 지원합니까? Adobe Primetime 인증은 온라인 소스에서 유료 TV 고객에게 비디오를 제공하기 위한 기술 요구 사항과 아키텍처를 제공하는 CableLabs OLCA(Online Content Access) 사양을 준수합니다. Adobe은 2011년 6월에 공동 CableLabs 옵트 테스트 프로젝트에 참여했으며 서비스 공급자 구현을 위한 테스트 프로세스를 통과했습니다. 인증을 위해 OLCA 사양에 대해 Adobe Primetime 인증이 확인(완료 및 테스트)됩니다. 인증 구성 요소가 완료되었으나 테스트 검증은 현재 CableLabs 테스트 환경의 릴리스를 기다리고 있습니다. 또한 Adobe은 OATC(Open Authentication Technical Consortium)의 활성 구성원이며, 해당 기관의 일부로서 몇 가지 분과위원회 사양 작성 프로젝트에 참여하고 있습니다.



인증이란 무엇입니까? 인증은 MVPD가 지정된 사용자가 알려진 고객임을 확인하는 프로세스입니다.



승인이란 무엇입니까? 권한 부여는 MVPD가 인증된 사용자가 지정된 리소스에 대한 유효한 구독을 가지고 있음을 확인하는 프로세스입니다.



## 아키텍처 {#architecture}

Adobe Primetime 인증은 MVPD와 프로그래머 모두에서 필요로 하는 비즈니스 규칙에 따라 신속한 백엔드(서버 간) 통합을 허용하는 호스팅 서비스입니다. 즉, 더 많은 플랫폼에서 더 많은 사람들이 사용할 수 있는 더 많은 TV 콘텐츠를 제공함으로써 모든 당사자를 위한 시장 출시 시기, 사기를 방지하기 위한 더 안전한 환경 및 우수한 고객 경험을 제공할 수 있습니다.


Adobe Primetime 인증은 SaaS(Software as a Service) 모델을 통해 제공되며, 컨텐츠에 대한 권한 부여를 확인하기 위해 최종 사용자, MVPD 및 프로그래머 간에 보다 안전한 커뮤니케이션을 수행할 수 있도록 합니다. 서비스의 핵심 구성 요소는 다음과 같습니다.

서버 측 - 호스팅된 Adobe Primetime 인증 서버입니다. MVPD의 인증 시스템과 역채널(서버 간) 통신을 수행하는 응용 프로그램 서버입니다.
고객측: 클라이언트측 액세스 Enabler - Access Enabler는 Programmer 웹 페이지 또는 플레이어 애플리케이션에 로드되는 작은 파일입니다. Programmer의 컨텐츠 보기 애플리케이션에 자격 부여 API를 제공하고 Adobe Primetime 인증 서버와 통신합니다.
Clientless 웹 서비스(웹이 불가능한 장치의 경우) - Smart TV, 게임 콘솔 및 셋톱 박스 등의 장치에 대한 자격 부여 API를 제공하는 RESTful 웹 서비스입니다.

>[!NOTE]
>
>MVPD인 웹 서비스는 Adobe Primetime 인증에서 인증 및 권한 부여에 대한 요청을 인식하고 필요한 데이터에 필요한 형식을 지정하여 응답할 수 있어야 합니다.

Adobe Primetime 인증을 사용하면 SSO(Single Sign-On) 인증 및 인증이라고도 하는 페더레이션 id 관리를 고객에게 제공할 수 있습니다. Adobe Primetime 인증을 사용할 때는 MVPD에서 인증을 유지하는 한 구독자가 첫 번째 인증 후 다시 로그인할 필요가 없습니다. (일반적으로 30일) 이를 위해 Adobe Primetime 인증은 고객의 인증 토큰을 위한 공통 도메인을 제공합니다. 이 인증 상태 정보는 지정된 MVPD와 통합된 모든 참여 사이트에서 사용할 수 있습니다.


현재 MVPD와의 대부분의 Adobe Primetime 인증 통합에서는 기본 인증 표준 중 하나인 SAML 프로토콜을 사용합니다. Adobe Primetime 인증은 SAML 아키텍처에서 프록시 서비스 공급자 역할을 하며 Adobe 공통 도메인에서 보안 토큰으로 SAML 인증 응답을 유지합니다. Adobe Primetime 인증은 SAML 2.0 준수입니다. 그러나 Adobe Primetime 인증은 일반적으로 이 시점에서 SAML SSO 솔루션에서 사용되지만 Adobe Primetime 인증 아키텍처는 특정 프로토콜에 바인딩되지 않습니다. 따라서 OAuth 2.0 또는 사용자 지정 프로토콜 기반의 프로토콜과 같은 새 프로토콜에 대한 지원은 시간에 따라 추가할 수 있습니다.


Adobe은 MVPD의 기술 팀과 협력하여 기존 통합의 요구를 충족하도록 Adobe Primetime 인증을 구성합니다. 통합은 &quot;표준&quot; 통합과 최소한의 지원 요구 사항(설명서 및 기본 이메일 지원)이 있다고 가정할 경우 MVPD에 대해 무료로 제공됩니다. MVPD에 상당한 지원 또는 문제 제기된 타임라인이 필요한 경우 지원 비용이 청구되거나 공급자가 Synacor와 같은 Adobe 솔루션을 잘 알고 있는 타사와 작업하려고 할 수 있습니다.


Adobe Primetime 인증은 다음과 같이 MVPD 비즈니스 로직을 효율적으로 처리할 수 있도록 지원합니다.

권한 부여 요청을 받을 때 MVPD가 직접 포함되고 적용할 수 있는 비즈니스 로직의 경우, Adobe은 MVPD가 권한 부여 요청을 받을 때 비즈니스 로직 수행을 지원하는 데 필요한 데이터를 제공합니다. 이 데이터에는 요청을 하는 사용자의 고유 장치 ID와 장치의 IP 주소를 포함할 수 있지만 이에 제한되지 않습니다.

Adobe 솔루션의 사용자 개입 및/또는 특정 처리를 필요로 하는 비즈니스 로직의 경우 Adobe은 각 MVPD에 대한 일부 사용자 지정 속성을 유지 관리할 수 있습니다. 이러한 MVPD별 구성/정책에는 최상위 워크플로우의 특정 지점에서 시작할 수 있는 사전 정의된 워크플로우의 활성화가 포함됩니다. 사용자 지정 속성 지원에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

다음 다이어그램은 이러한 Adobe Primetime 인증 구성 요소를 사용하는 MVPD 및 프로그래머의 관계를 보여줍니다.

![](assets/high-level-architecture-nflows.png)

*그림: 높은 수준의 아키텍처 및 흐름*

## Adobe Primetime 인증 구성 요소 {#components}

다음은 Adobe Primetime 인증 환경 시스템의 일부 주요 구성 요소에 대한 개요를 제공합니다. 다음과 같은 보고서가 포함됩니다.

* [Access Enabler / Clientless Web Services](#ae)
* [Adobe 호스팅 백엔드 서버](#backend)
* [토큰](#tokens)

### Access Enabler / Clientless Web Services {#ae}

Access Enabler는 사용자와 모든 인증 및 인증 상호 작용을 용이하게 하며 해당 시스템에서 로컬로 실행됩니다. MVPD를 사용하여 실제 자격 워크플로우를 처리하는 Access Enabler와, 프로그래머는 상위 수준 웹 페이지 또는 플레이어 애플리케이션에 대한 책임을 유지합니다.

클라이언트 없는 웹 서비스는 웹 페이지를 렌더링할 수 없는 장치에 대해 Adobe Primetime 인증에서 제공합니다.  이러한 장치의 경우, 자격 프로세스가 시작되고 스마트 장치에서 보이는 컨텐츠가 수행되는 반면, MVPD와의 인증은 웹 가능 장치(PC, 스마트폰 및 태블릿)에서 수행됩니다.

Access Enabler:

* MVPD별 인증 및 인증 워크플로우를 시작합니다.
* 프로그래머 리소스/채널당 성공적인 인증 응답을 캐시하여 불필요한 요청 트래픽을 최소화합니다.
* 명시적 장치 등록과 같이 각 MVPD에 해당하는 사전 정의된 워크플로우에 대해 구성할 수 있습니다.
* 다음 양식에서 사용할 수 있습니다.
   * Flash Player 런타임에서 실행할 수 있는 SWF 파일입니다
   * 브라우저에 의해 직접 실행되는 JS 파일
   * iOS, Android 및 Xbox 등 다양한 플랫폼에 대한 기본 액세스 Enabler

### Adobe 호스팅 백엔드 서버 {#backend}

Adobe에 의해 호스팅되는 Adobe Primetime 인증 백엔드 서버:

* Adobe Primetime 인증과 운영자 간에 서버 간 통신이 필요한 MVPD를 사용하여 인증 및 인증 워크플로우를 규정합니다.
* 프로그래머 사이트 및 응용 프로그램의 구성을 유지 관리합니다.
* 다운로드 가능한 Access Enabler 구성 요소 파일을 호스팅합니다.
* 인증 및 인증 토큰을 생성합니다.

### 토큰 {#tokens}

Adobe Primetime 인증 자격 솔루션은 인증/인증 워크플로우가 성공적으로 완료될 때 획득되는 특정 데이터 조각을 생성하는 데 중점을 둡니다. 이러한 데이터 조각을 토큰이라고 합니다. 수명이 제한되어 플랫폼 종속 위치에 안전하게 저장됩니다. 만료 시 인증 및/또는 인증 워크플로우의 재시작을 통해 토큰을 다시 발급해야 합니다.

인증/인증 워크플로우 중에 실행되는 토큰은 세 가지 유형이 있습니다. 두 가지는 &quot;장기간&quot;이며, 사용자의 보기 경험에 연속성을 제공합니다. 세 번째, 수명이 짧은 토큰은 스트림 리핑을 통해 사기를 완화하기 위한 업계 우수 사례를 지원합니다. 토큰의 TTL(time-to-live) 값은 MVPD와 프로그래머 간의 계약에 따라 설정됩니다. 비즈니스 및 고객에게 가장 적합한 TTL 값을 결정합니다.

**장기간 인증 토큰**. 고객이 Adobe Primetime 인증을 사용하여 MVPD 계정에 성공적으로 로그온하면 인증 작업이 수행됩니다. 그러면 Adobe Primetime 인증에서는 요청 장치에 연결된 장기화된 인증(&quot;authN&quot;) 토큰을 생성하고(MVPD에 따라) 사용자를 익명으로 식별하는 전역적 고유 식별자(&quot;GUID&quot;)를 생성합니다.

**장기간 인증 토큰**. 성공적으로 인증되면 Adobe Primetime 인증은 장기간 인증(&quot;authZ&quot;) 토큰을 만듭니다. 이 토큰은 요청 장치 및 특정 보호 리소스(예: 채널, 시리즈 또는 에피소드)에 연결되어 있으므로 휴대할 수 없습니다. Access Enabler는 오랫동안 사용하던 authZ 토큰을 사용하여 실제 보기 액세스에 사용되는 단기 미디어 토큰을 만듭니다.

**단기 미디어 토큰**. 사용자가 인증되면 Adobe Primetime 인증은 authZ 토큰을 생성하고 이 토큰을 사용하여 Adobe에 의해 서명되고 교환 중 탬퍼링을 방지하기 위해 암호화된 단기간 사용 미디어 토큰을 생성합니다. 단기 토큰은 Access Enabler API 또는 Clientless 웹 서비스 중 하나를 통해 포함 사이트에 노출되므로 보호된 리소스에 대한 액세스를 제공하기 전에 Programmer의 미디어 서버는 Adobe Primetime 인증 구성 요소인 Media Token Verifier를 사용하여 토큰의 유효성을 검사해야 합니다.

## MVPD 통합 라이프사이클 {#lifecycle}

다음 그림은 Adobe Primetime 인증과 MVPD 간의 통합 주기를 보여줍니다.

![](assets/mvpd-int-lifecycle.png)

*그림: MVPD 통합 라이프사이클*

## 자격 순서도 {#chart}

다음 순서도는 Adobe Primetime 인증을 사용하여 자격 증명을 확인하는 전반적인 프로세스를 보여 줍니다.

![](assets/authn-authz-entitlmnt-flow.png)

*그림: Adobe Primetime 인증을 사용하여 자격 확인을 수행하는 프로세스입니다*

## 인증 단계 {#authn-steps}

다음 단계에서는 Adobe Primetime 인증 흐름의 예를 보여줍니다.  프로그래머가 사용자가 MVPD의 유효한 고객인지 확인하는 자격 프로세스의 일부입니다.  이 시나리오에서는 사용자가 MVPD의 유효한 가입자입니다.  사용자가 Programmer의 Flash 응용 프로그램을 사용하여 보호된 콘텐츠를 보려고 합니다.

1. 사용자가 Programmer의 웹 페이지로 이동하여 Programmer의 Flash 응용 프로그램 및 Adobe Primetime 인증 Access Enabler 구성 요소를 사용자 시스템으로 로드합니다. Flash 응용 프로그램은 Access Enabler를 사용하여 Programmer의 ID를 Adobe Primetime 인증으로 설정하고 Adobe Primetime 인증은 Access Enabler를 해당 Programmer(&quot;요청자&quot;)의 구성 및 상태 데이터로 설정합니다. Access Enabler는 다른 API 호출을 수행하기 전에 서버에서 이 데이터를 수신해야 합니다.  기술 참고 사항: 프로그래머는 Access Enabler를 사용하여 ID 설정 `setRequestor()` 메서드 자세한 내용은 [Programmer Integration 안내서](/help/authentication/programmer-integration-guide-overview.md).
1. 사용자가 Programmer의 보호된 콘텐츠를 보려고 하면 Programmer의 응용 프로그램은 사용자가 공급자를 선택할 MVPD 목록을 사용자에게 표시합니다.
1. 사용자가 선택한 MVPD에 대한 암호화된 SAML 요청이 생성된 Adobe Primetime 인증 서버로 사용자가 리디렉션됩니다. 이 요청은 프로그래머를 대신하여 MVPD에게 인증 요청으로 전송됩니다. MVPD 시스템에 따라 사용자의 브라우저는 MVPD 사이트로 리디렉션되어 로그인하거나 Programmer의 앱에서 로그인 iFrame을 만듭니다.
1. 어느 경우든(리디렉션 또는 iFrame) MVPD가 요청을 수락하고 로그인 페이지를 표시합니다.
1. 사용자가 MVPD로 로그인하고 MVPD가 유료 고객으로서의 사용자 상태를 확인한 다음 MVPD가 자체 HTTP 세션을 만듭니다.
1. 사용자의 유효성을 검사하면 MVPD는 MVPD가 Adobe Primetime 인증으로 다시 보내는 응답(SAML 및 암호화)을 만듭니다.
1. Adobe Primetime 인증은 MVPD 응답을 수신하고, Adobe Primetime 인증 HTTP 세션이 열려 있는지 확인하고, [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) MVPD의 응답을 수신하고 다시 프로그래머 사이트로 리디렉션합니다.
1. Programmer의 사이트가 다시 로드되고 Access Enabler가 다시 로드되고 Programmer가 setRequestor()를 다시 호출합니다.  현재 구성이 변경되었기 때문에 setRequestor()에 대한 두 번째 호출이 필요합니다. 이제 Access Enabler에 서버에서 AuthN 토큰이 생성되기를 기다리고 있음을 알리는 플래그가 있습니다.
1. Access Enabler는 보류 중인 인증이 있음을 확인하고 Adobe Primetime 인증 서버에서 토큰을 요청합니다. 토큰은 Flash Player의 DRM 기능을 호출하여 서버에서 검색됩니다.
1. AuthN 토큰은 Programmer의 Flash Player LSO 캐시에 저장됩니다. 이제 인증이 완료되고 세션이 Adobe Primetime 인증 서버에서 제거됩니다.

## 인증 단계 {#authz-steps}

다음 단계는 이전 섹션([인증 단계](#authn-steps)):

1. 사용자가 Programmer의 보호된 콘텐츠에 액세스하려고 하면 Programmer의 애플리케이션은 사용자의 로컬 시스템 또는 장치에서 AuthN 토큰을 먼저 확인합니다.  해당 토큰이 없으면 [인증 단계](#authn-steps) 위의 항목이 따릅니다.  AuthN 토큰이 있는 경우 권한 부여 플로우는 보호된 컨텐츠의 특정 항목에 대한 사용자의 보기 권한을 가져오도록 요청하여 Access Enabler에 대한 호출을 시작하는 Programmer의 응용 프로그램으로 진행됩니다.
1. 보호된 컨텐츠의 특정 항목은 &quot;리소스 식별자&quot;로 표시됩니다.  간단한 문자열이거나 더 복잡한 구조일 수 있지만, 어떤 경우든, Programmer와 MVPD 간에 미리 리소스 식별자의 특성에 대해 동의됩니다.  Programmer의 응용 프로그램은 리소스 식별자를 Access Enabler로 전달합니다.  Access Enabler는 사용자의 로컬 시스템 또는 장치에서 AuthZ 토큰을 확인합니다.  AuthZ 토큰이 없으면 Access Enabler가 요청을 백엔드 Adobe Primetime 인증 서버에 전달합니다.
1. Adobe Primetime 인증 서버는 표준화된 프로토콜을 사용하여 MVPD의 인증 종단점과 통신합니다.  MVPD의 응답에 보호된 콘텐츠를 볼 수 있는 권한이 사용자에게 있음을 나타내는 경우 Adobe Primetime 인증 서버는 AuthZ 토큰을 만들어 사용자 컴퓨터에 AuthZ 토큰을 저장하는 Access Enabler로 다시 전달합니다.
1. 사용자의 시스템 또는 장치에 저장된 AuthZ 토큰을 사용하여 Programmer의 애플리케이션은 Access Enabler를 호출하여 Adobe Primetime 인증 서버에서 미디어 토큰을 가져오고 해당 토큰을 Programmer의 애플리케이션에 제공합니다.
1. 마지막으로, Programmer의 응용 프로그램은 미디어 토큰 확인기 구성 요소를 사용하여 올바른 사용자가 올바른 컨텐츠를 보고 있는지 확인하고, 미디어 토큰을 제자리에 두고 사용자는 보호된 콘텐츠를 볼 수 있습니다.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
