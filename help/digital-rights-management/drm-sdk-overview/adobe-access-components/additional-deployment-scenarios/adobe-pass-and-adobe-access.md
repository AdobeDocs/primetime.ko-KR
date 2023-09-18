---
title: Adobe Primetime 인증 및 Adobe Primetime DRM
description: Adobe Primetime 인증 및 Adobe Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Adobe Primetime 인증 및 Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

Adobe Primetime 인증( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/))는 여러 콘텐츠 제공자에 걸쳐 사용자/장치 인증 및 권한 부여를 제공합니다. 사용자에게 유효한 케이블 TV 또는 위성 TV 구독이 있어야 합니다.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Primetime 인증은 미디어 콘텐츠를 보호하기 위한 Adobe Primetime DRM과 함께 사용할 수 있습니다. 이 시나리오에서 비디오 플레이어(SWF)는 라는 다른 SWF을 로드할 수 있습니다. *액세스 Enabler*: Adobe Systems에 의해 호스팅됩니다. 다음 *액세스 Enabler* 는 Adobe Primetime 인증 서비스에 연결하고 SAML SSO를 MVPD(다채널 비디오 프로그래밍 배포자) ID 공급자 시스템과 쉽게 통합하는 데 사용됩니다. 여기에는 사용자의 브라우저를 잠시 MVPD 로그인 페이지로 리디렉션한 다음 AuthN 토큰을 유지하고 마지막으로 캐시된 AuthN 세션을 사용하여 콘텐츠 웹 사이트로 돌아가는 작업이 포함됩니다.

다음 *액세스 Enabler* 그런 다음 Adobe Primetime 인증 서비스와 MVPD 간에 백엔드 승인을 용이하게 할 수 있습니다. MVPD는 비즈니스 논리를 유지하고 사용자가 받을 수 있는 콘텐츠를 결정합니다. 권한은 해당 콘텐츠 리소스에 대한 추가 AuthZ 토큰에서 유지되며 클라이언트로 다시 전송됩니다.

인증 및 권한 부여 토큰은 Primetime DRM 클라이언트의 고유 ID 및 개인 키를 사용하여 서명되어 변조 또는 스푸핑을 방지합니다. 이 토큰은 *액세스 Enabler*.

비디오 플레이어는 를 호출하여 프로세스를 트리거할 수 있습니다. `getAuthorization` 다음에 있음 *액세스 Enabler*. 유효한 AuthN/AuthZ 토큰이 있으면 *액세스 활성* 비디오 컨텐츠를 재생하기 위해 단기 미디어 토큰을 포함할 콜백을 비디오 플레이어에 발행합니다.

Adobe Primetime 인증은 서버에 배포할 수 있는 미디어 토큰 유효성 검사기 Java 라이브러리를 제공합니다. 컨텐츠 보호를 위해 Primetime DRM 서버를 사용하는 경우 미디어 토큰의 유효성을 검사한 후 미디어 토큰 유효성 검사기를 Primetime DRM 서버측 플러그인과 통합하여 일반 라이선스를 자동으로 발급할 수 있습니다. 그런 다음 콘텐츠는 CDN 서버에서 클라이언트로 스트리밍됩니다. 컨텐츠 라이센스를 취득하기 위해 단기 미디어 토큰을 Primetime DRM 서버에 제출하여 토큰의 유효성을 검증받고 라이센스를 발급받을 수 있다.

장기 AuthN 토큰은 일반적으로 *액세스 Enabler* 모든 콘텐츠 개발자가 해당 MVPD 구독자에 대한 AuthN을 나타냅니다. 또한 Primetime DRM 서버 및 토큰 검증기는 CDN 또는 콘텐츠 공급자를 대신하여 서비스 공급자가 운영할 수 있습니다.
