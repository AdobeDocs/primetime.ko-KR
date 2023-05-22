---
title: Adobe Primetime 인증 모니터링
description: Adobe Primetime 인증 모니터링
exl-id: fb000e9d-b5aa-45b1-a914-9e419ec8a4d9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Adobe Primetime 인증 모니터링 {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## 소개 {#intro}

고객은 다음을 사용할 수 있습니다 [나기오스](http://www.nagios.org) 또는 Adobe Primetime 인증이 설정되어 있는지 여부를 확인하는 기타 도구입니다. 

## 엔드포인트 모니터링 {#monitoring-endpoints}

### 모니터링할 수 있는 엔드포인트 {#endpoints-to-monitor}

* 모든 플랫폼에 대한 구성 끝점: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- HTTP 또는 HTTPS를 통해 사용할 수 있습니다(콘텐츠 제공업체의 개발자가 선택한 사항에 따라 다름). 이 끝점이 없으면 모든 플랫폼 및 모든 MVPD에서 콘텐츠를 사용할 수 없게 됩니다. Clientless REST API의 경우 다음 엔드포인트도 있습니다.  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* 다음 종단점은 Adobe Primetime 인증 웹 SDK의 일부입니다.  누락된 경우 모든 프로그래머 및 모든 웹 속성에 대해 pay-TVpass가 다운되었음을 의미합니다.

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### 모니터링해서는 안 되는 엔드포인트 {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   이 끝점에는 MVPD SAML 응답이 필요하므로 항상 503 오류가 발생합니다.

* 기타 자격 엔드포인트 - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

관련 회신에 대한 페이로드가 필요하므로 이러한 끝점을 모니터링할 수 없습니다.
