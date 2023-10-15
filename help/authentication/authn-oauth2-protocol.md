---
title: OAuth 2.0 프로토콜을 사용한 인증
description: OAuth 2.0 프로토콜을 사용한 인증
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# OAuth 2.0 프로토콜을 사용한 인증

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## 개요 {#overview}

여전히 SAML이 미국의 MVPD와 기업에서 인증에 사용되는 주요 프로토콜이지만, 주 인증 프로토콜로 OAuth 2.0으로 이동하는 경향이 뚜렷합니다. OAuth 2.0 프로토콜(https://tools.ietf.org/html/rfc6749)은 주로 소비자 사이트를 위해 개발되었으며 Facebook, Google 및 Twitter과 같은 인터넷 거대기업이 신속하게 채택했습니다.

OAuth 2.0은 매우 성공적이므로 기업은 이를 지원하기 위해 인프라를 천천히 업그레이드해야 합니다.



## OAuth 2.0으로 이동할 때의 이점 {#adv-oauth2}

높은 수준에서 OAuth 2.0 프로토콜은 SAML 프로토콜과 동일한 기능을 제공하지만 몇 가지 중요한 차이점이 있습니다.

이러한 이유 중 하나는 바로 뒤에서 인증을 새로 고치는 방법으로 새로 고침 토큰 플로우를 사용할 수 있다는 사실입니다. 이를 통해 IdP(이 경우 MVPD)는 제어를 유지하면서도 보안 문제로 인해 더 이상 자주 로그인할 필요가 없으므로 양호한 사용자 경험을 계속 사용할 수 있습니다.

또한 프로토콜은 서비스 제공자가 토큰을 사용하여 추가 정보를 얻기 위해 다른 API에 액세스할 수 있으므로 노출된 데이터에 대해 더 많은 유연성을 제공합니다. 결과적으로 TVE 사용 사례에 대한 &quot;chattier&quot; 프로토콜이 생성되지만 복잡한 워크플로우에 필요한 유연성을 제공합니다.





## OAuth 2.0으로 전환하기 위한 요구 사항 {#oauth-req}

OAuth 2.0을 통한 인증을 지원하려면 MVPD가 다음 사전 요구 사항을 충족해야 합니다.

무엇보다도 MVPD가 다음을 지원하는지 확인해야 합니다. [인증 코드 부여](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) 흐름.

MVPD는 흐름을 지원함을 확인한 후 다음과 같은 정보를 제공해야 합니다.

* 인증 끝점
   * 끝점은 나중에 새로 고침 및 액세스 토큰의 exchange에서 사용할 인증 코드를 제공합니다.
* /token 끝점
   * 새로 고침 토큰 및 액세스 토큰을 제공합니다.
   * 새로 고침 토큰은 안정적이어야 합니다(새 액세스 토큰을 요청할 때마다 변경해서는 안 됨).
   * mvpd는 각 새로 고침 토큰에 대해 여러 개의 활성 액세스 토큰을 허용해야 합니다
   * 이 끝점은 또한 새로 고침 토큰을 액세스 토큰으로 교환합니다.
* 다음 항목이 필요합니다. **사용자 프로필의 끝점**
   * 이 종단점은 계정에 대해 고유해야 하며 개인 식별 정보를 포함해서는 안 되는 userID를 제공합니다
* 다음 **/logout** 끝점(선택 사항)
   * Adobe Primetime 인증은 이 끝점으로 리디렉션하고 MVPD에 리디렉션 백 URI를 제공합니다. 이 끝점에서 MVPD는 클라이언트 컴퓨터의 쿠키를 지우거나 로그아웃에 원하는 논리를 적용할 수 있습니다
* 승인된 클라이언트(사용자 인증 페이지를 트리거하지 않는 클라이언트 앱)를 지원하는 것이 좋습니다
* 필요한 사항은 다음과 같습니다.
   * **clientID** 및 **클라이언트 암호** 통합 구성용
   * **살 수 있는 시간** 새로 고침 토큰 및 액세스 토큰에 대한 TTL(값)
   * Authorization 콜백 및 로그아웃 콜백 URI를 MVPD에 제공할 수 있습니다. 또한 필요한 경우 MVPD에 방화벽 설정에서 화이트리스트에 추가할 IP 목록을 제공할 수 있습니다.


## 인증 흐름 {#authn-flow}

인증 흐름에서 Adobe Primetime 인증은 구성에서 선택한 프로토콜의 MVPD와 통신합니다. OAuth 2.0 흐름은 아래 그림에 나와 있습니다.



![구성에서 선택한 프로토콜의 MVPD와 통신하는 Adobe 인증의 인증 흐름을 보여 주는 다이어그램입니다.](assets/authn-flow.png)

**그림 1: OAuth 2.0 인증 흐름**



## 인증 요청 및 응답 {#authn-req-response}

간단히 말해, OAuth 2.0 프로토콜을 지원하는 MVPD에 대한 인증 흐름은 다음 단계를 따릅니다.

1. 최종 사용자는 프로그래머 사이트로 이동하여 MVPD 자격 증명으로 로그인하도록 선택합니다
1. 프로그래머 측에 설치된 AccessEnabler는 HTTP 요청 형태로 인증 요청을 Adobe Primetime 인증 엔드포인트로 보내고, Adobe Primetime 인증 엔드포인트는 MVPD 인증 엔드포인트로 리디렉션합니다.
1. MVPD 인증 끝점이 Adobe Primetime 인증 끝점에 인증 코드를 보냅니다.
1. Adobe Primetime 인증은 수신된 인증 코드를 사용하여 MVPD의 토큰 엔드포인트에서 새로 고침 토큰과 액세스 토큰을 요청합니다
1. 사용자 정보가 토큰에 포함되지 않은 경우 사용자 프로필 끝점에 사용자 정보 및 메타데이터 가져오기 호출을 보낼 수 있습니다
1. 이제 프로그래머 사이트를 성공적으로 검색할 수 있는 최종 사용자에게 인증 토큰이 전달됩니다

   >[!NOTE]
   >
   >새로 고침 토큰은 현재 액세스 토큰이 잘못되거나 만료된 후 새 액세스 토큰을 가져오는 데 사용됩니다.


>[!IMPORTANT]
>
>새로 고침 토큰은 액세스 토큰과 교환될 때 변경되지 않아야 합니다.

이 제한은 서버가 OAuth 2.0 프로토콜의 경우 새로 고침 토큰도 포함하는 AuthNToken을 업데이트할 수 없는 클라이언트 흐름에서 비롯됩니다.

일반적인 인증 흐름은 AuthNToken에 저장된 새로 고침 토큰을 액세스 토큰으로 교환하고, 액세스 토큰은 처음에 인증된 사용자의 이름으로 인증 호출을 수행하는 데 사용됩니다. 인증 서버(MVPD)가 새로 고침 토큰을 변경하고 이전 토큰을 무효화하면 유효한 AuthNToken을 업데이트할 수 없습니다. 이러한 이유로 MVPD는 안정적인 새로 고침 토큰을 지원해야 OAuth 2.0 통합을 설정할 수 있습니다.


## SAML에서 OAuth 2.0으로 마이그레이션 {#saml-auth2-migr}

SAML에서 OAuth 2.0으로 통합을 마이그레이션하는 작업은 Adobe 및 MVPD에서 수행합니다. 프로그래머가 MVPD 로그인 페이지에서 공동 브랜딩을 확인/테스트할 수 있지만 프로그래머 측에서는 기술 변경이 필요하지 않습니다. MVPD의 관점에서 보면 Oauth 2.0 요구 사항에서 요청한 엔드포인트와 기타 정보가 필요합니다.

에게 **sso 유지**, 이미 SAML을 통해 얻은 인증 토큰이 있는 사용자는 여전히 인증된 것으로 간주되며 해당 요청은 이전 SAML 통합을 통해 라우팅됩니다.

기술적 관점에서

1. Adobe은 SAML 통합을 삭제하지 않고 프로그래머와 MVPD 간에 OAuth 2.0 통합을 활성화합니다.
1. 활성화하면 모든 신규 사용자가 OAuth 2.0 흐름을 사용하게 됩니다.
1. 이미 SAML 주체-ID가 포함된 로컬 AuthN 토큰이 있는 사용자는 SAML 통합을 통해 Adobe에 의해 자동으로 라우팅됩니다.
1. 3단계의 사용자의 경우 SAML에서 생성한 AuthN 토큰이 만료되면 Adobe은 해당 사용자를 새 사용자로 취급하고 2단계의 사용자처럼 동작합니다.
1. Adobe은 SAML 통합을 안전하게 비활성화할 수 있는 순간을 결정하기 위해 사용 패턴을 검토합니다.