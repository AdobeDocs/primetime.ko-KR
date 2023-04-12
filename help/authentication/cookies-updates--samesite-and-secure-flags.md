---
title: 쿠키 업데이트 - SameSite 및 Secure 플래그
description: 쿠키 업데이트 - SameSite 및 Secure 플래그
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# 쿠키 업데이트 - SameSite 및 Secure 플래그 {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


## 업데이트 {#Updates}

이 섹션에서는 타사 쿠키를 처리하기 위해 Chrome 브라우저 및 Adobe Primetime 인증에 의해 도입된 변경 사항을 강조 표시합니다.

 

### Chrome 80 업데이트 {#Chrome}

Chrome 버전 80(버전 82 제외)부터 는 *SameSite* 속성은 속성이 *SameSite=Lax*. 따라서 사이트 간 컨텍스트에서 전달해야 하는 쿠키는 명시적으로 *SameSite=None*, 및에 *보안* 특성 및 전달 *HTTPS*. 이러한 업데이트에 대한 자세한 내용은 공식 chromium 페이지에서 확인할 수 있습니다. <https://www.chromium.org/updates/same-site> 다음에서 <https://web.dev/samesite-cookies-explained/>.


### Adobe Primetime 인증 업데이트 {#Pass-Updates}

Adobe Primetime 인증 서비스는 현재 일부 플랫폼 및 Adobe Primetime 인증 SDK의 버전과 함께 작동하기 위해 브라우저의 관점에서 타사 쿠키로 간주되는 두 개의 쿠키에 의존하고 있습니다. 따라서 Adobe Primetime 인증 서비스는 예정된 변경 사항을 준수하고 이러한 이전 SDK의 사이트 간 컨텍스트에서 이러한 쿠키를 계속 제공하기 위해 *adobe-pass-2.55.1* 버전.

이러한 변경 사항은 *adobe-pass-2.55.1* 버전은 *보안* 및 *SameSite=None* 버전 80 이상(버전 82 제외)으로 시작하는 Chrome 브라우저를 사용할 때 모든 Adobe Primetime 인증 SDK에 전달된 모든 해당 쿠키의 속성입니다.

다음 섹션에서는 한 사용자가 Chrome 브라우저 80 이상(버전 82 제외)을 사용하는 경우 플랫폼 및 Adobe Primetime 인증 SDK 버전 목록에 대한 몇 가지 잠재적인 문제를 설명합니다.

## 문제 해결 {#Troubleshooting}

이 섹션을 검색하는 동안 모든 Adobe Primetime 인증 서비스 쿠키에는 *보안* 속성 설정 *adobe-pass-2.55.1* 모든 브라우저에 대해 버전을 지원하는 반면, *SameSite=None* 속성은 Chrome 브라우저 버전 80 이상(버전 82 제외)에 대해서만 설정되어야 합니다.


### 일반 문제 해결 {#General}

1. 일부 사용자 에이전트가 *SameSite=None* 속성을 사용합니다.

   - Chrome 51에서 Chrome 66으로(양쪽에 포함) Chrome 버전. 이러한 Chrome 버전은 *SameSite=None*. 이 기능은 Android WebView뿐만 아니라 이전 버전의 Chromium 파생 브라우저에도 영향을 줍니다. 이 동작은 당시 쿠키 사양의 버전에 따라 정확했으나 사양에 새 &quot;없음&quot; 값을 추가하여 Chrome 67 이상에서 업데이트되었습니다. (Chrome 51 이전에는 SameSite 속성이 완전히 무시되었으며 모든 쿠키가 실제 쿠키인 것처럼 처리되었습니다 *SameSite=None*)
   - 버전 12.13.2 이전 버전의 Android에서 UC 브라우저 버전입니다. 이전 버전은 *SameSite=None*. 이 동작은 당시 쿠키 사양의 버전에 따라 정확했지만 사양에 새로운 &quot;없음&quot; 값을 추가하여 이 동작이 최신 버전의 UC 브라우저에서 업데이트되었습니다.
   - MacOS 10.14 및 iOS 12의 모든 브라우저에 Safari 및 포함된 브라우저 버전. 이러한 버전은 *SameSite=None* 마치 *SameSite=Strict*. 이 버그는 최신 버전의 iOS 및 MacOS에서 수정되었습니다.


1. 쿠키에 *보안* 속성을 전송해야 합니다. *HTTPS*&#x200B;를 선택하지 않으면 쿠키가 Adobe Primetime 인증 서비스에 도달하지 않습니다.

   - AccessEnabler JavaScript SDK:
      - 통신과 관련하여 *sp.auth.adobe.com* 사용 *HTTPS* 버전 *2.35* 및 *3.5.0*: Dynamic Client Registration을 도입하기 전에
   - AccessEnabler iOS/tvOS SDK:
      - 통신과 관련하여 *sp.auth.adobe.com* 사용 *HTTPS* 이전 버전의 경우 *3.0.0*: Dynamic Client Registration을 도입하기 전에
   - AccessEnabler Android SDK:
      - 통신과 관련하여 *sp.auth.adobe.com* 사용 *HTTPS* 이전 버전의 경우 *3.0.0*: Dynamic Client Registration을 도입하기 전에
   - AccessEnabler FireOS SDK:
      - 통신과 관련하여 *sp.auth.adobe.com* 사용 *HTTPS* 버전 *2.0.4*.

</br>

### AccessEnabler JavaScript SDK 버전 2.35 문제 해결 {#235-Troubleshooting}

사용자의 인증 흐름은 Chrome 80 이상(버전 82 제외)에서 영향을 받을 수 있습니다. 위의 업데이트로 인해 사용자에게 인증을 받을 문제가 없는지 확인하기 위해 다음을 수행할 수 있습니다.

- 다음을 확인하십시오. *JSESSIONID* 쿠키는 브라우저에서 설정되고 *SameSite=None* 및 *보안* 속성 세트. 
- 다음을 확인하십시오. *JSESSIONID* 쿠키의 *https://sp.auth.adobe.com/authenticate/saml* 네트워크 요청이 일치함 *JSESSIONID* 쿠키의 *https://sp.auth.adobe.com/session* 네트워크 요청.


### AccessEnabler JavaScript SDK 버전 3.5.0 문제 해결 {#350-Troubleshooting}

사용자의 인증 흐름은 Chrome 80 이상(버전 82 제외)에서 영향을 받을 수 있습니다. 위의 업데이트로 인해 사용자에게 인증을 받을 문제가 없는지 확인하기 위해 다음을 수행할 수 있습니다.

- 다음을 확인하십시오. *JSESSIONID* 쿠키는 브라우저에서 설정되고 *SameSite=None* 및 *보안* 속성 세트. 
- 다음을 확인하십시오. *JSESSIONID* 쿠키의 *https://sp.auth.adobe.com/authenticate/saml* 네트워크 요청이 일치함 *JSESSIONID* 쿠키의 *https://sp.auth.adobe.com/session* 네트워크 요청.
- 다음을 확인하십시오. *pass\_sfp* 쿠키는 브라우저에서 설정되고 *SameSite=None* 및 *보안* 속성 세트.
- 다음을 확인하십시오. *pass\_sfp* 쿠키가 *https://sp.auth.adobe.com/session* 네트워크 요청.


사용자의 인증 흐름은 Chrome 80 이상(버전 82 제외)에서 영향을 받을 수 있습니다. 위의 업데이트로 인해 인증된 후 사용자가 보호된 리소스를 보는 데 문제가 없는지 확인하기 위해 다음을 수행할 수 있습니다.

- 다음을 확인하십시오. *pass\_sfp* 쿠키는 브라우저에서 설정되고 *SameSite=None* 및 *보안* 속성 세트.
- 다음을 확인하십시오. *pass\_sfp* 쿠키가 *https://sp.auth.adobe.com/adobe-services/authorize* 네트워크 요청.
- 다음을 확인하십시오. *pass\_sfp* 쿠키가 *https://sp.auth.adobe.com/adobe-services/shortAuthorize* 네트워크 요청.
