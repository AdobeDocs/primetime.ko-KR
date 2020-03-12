---
seo-title: Adobe Pass 및 Adobe Access
title: Adobe Pass 및 Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass 및 Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass( [](https://www.adobe.com/products/adobepass/))는 다양한 컨텐츠 제공업체에서 사용자/디바이스 인증 및 인증을 제공합니다. 유효한 케이블 TV 또는 위성 TV를 구독해야 합니다.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass는 미디어 컨텐츠를 보호하기 위해 Adobe Access와 함께 사용할 수 있습니다. 이 시나리오에서 비디오 플레이어(SWF)는 Adobe Systems에서 호스팅하는 액세스 *원동력이라는*&#x200B;다른 SWF를 로드할 수 있습니다. 액세스 *원동력* (Access Enabler)은 Adobe Pass 서비스에 연결하고 MVPD의 MVPD(Multichannel Video Programming Distributor) ID 공급자 시스템과의 SAML SSO 통합을 촉진하는 데 사용됩니다. 여기에는 사용자의 브라우저를 MVPD 로그인 페이지로 간단히 리디렉션한 다음 AuthN 토큰을 지속한 다음 마지막으로 캐시된 AuthN 세션을 사용하여 컨텐츠 웹 사이트로 돌아갑니다.

액세스 *원동력* (Access Enabler)은 Adobe Pass 서비스와 MVPD 간 백엔드 인증을 용이하게 합니다. MVPD 파섹 권한 부여는 해당 컨텐츠 리소스에 대한 추가 AuthZ 토큰에 유지되며 클라이언트로 다시 전송됩니다.

인증 및 인증 토큰은 변조 또는 스푸핑을 방지하기 위해 Adobe Access 클라이언트의 고유 ID 및 개인 키를 사용하여 서명됩니다. 이 토큰은 액세스 원동력(Access Enabler)을 통해서만 액세스할 수 *있습니다*.

비디오 플레이어는 액세스 원동력(Access Enabler) `getAuthorization` 을 호출하여 프로세스를 트리거할 *수 있습니다*. 유효한 AuthN/AuthZ 토큰이 있으면 *AccessEnabler* 가 비디오 컨텐츠를 재생하기 위해 짧은 기간 미디어 토큰을 포함하는 비디오 플레이어에 콜백을 발행합니다.

Adobe Pass는 서버에 배포할 수 있는 미디어 토큰 유효성 검사기 Java 라이브러리를 제공합니다. 컨텐츠 보호를 위해 Flash Access 서버를 사용하는 경우 미디어 토큰 유효성 검사기를 Adobe Access 서버측 플러그인과 통합하여 미디어 토큰의 유효성을 성공적으로 확인한 후 일반 라이센스를 자동으로 발행할 수 있습니다. 그러면 컨텐츠가 CDN 서버에서 클라이언트로 스트리밍됩니다. 컨텐츠 라이선스를 획득하기 위해 짧은 기간 동안의 미디어 토큰을 Adobe Access 서버에 제출할 수 있습니다. Adobe Access Server는 토큰의 유효성을 확인하고 라이선스를 발행할 수 있습니다.

오랫동안 사용되던 AuthN 토큰은 일반적으로 모든 컨텐츠 *개발자의* Access Enabler가 해당 MVPD 구독자에 대한 AuthN을 나타내는 데 사용됩니다. 또한 Adobe Access Server 및 Token Verifier는 컨텐츠 제공자를 대신하여 CDN 또는 서비스 제공업체가 수행할 수 있습니다.
