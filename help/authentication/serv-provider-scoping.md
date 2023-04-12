---
title: 서비스 공급자 범위 지정
description: 서비스 공급자 범위 지정
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 서비스 공급자 범위 지정 {#service-provoider-scoping}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#overview}

MVPD와 Adobe Primetime 인증 통합의 기본 구현은 **OLCA 사양**. OLCA 사양(6.5, 주체 식별자)의 인증 요구 사항 섹션에서는 주체 식별자에 대한 SP(서비스 제공자)의 범위 지정을 나타낼 수 있다고 설명합니다. (주체 식별자는 MVPD가 SP로 반환하는 난독화된 사용자 ID입니다.)  Adobe Primetime 인증 통합에서 MVPD가 SP 인증 요청 범위 지정을 활성화해야 합니다.

프로그래머용 SP 역할을 수행하는 Adobe Primetime 인증을 통해 인증 요청의 SP 범위 지정을 활성화하는 사용자 지정을 구현해야 합니다.  MVPD가 MVPD의 IDp(Identity Provider)에 SAML 어설션에서 전달된 네트워크 브랜드를 식별할 수 있도록 해야 합니다.  다음 섹션에 설명된 두 가지 방법 중 하나로 범위 지정을 구현할 수 있습니다.

## 서비스 공급자 범위 지정 {#service-provider-scoping}

Adobe Primetime 인증에서는 SP 범위 지정 인증 요청을 활성화하는 다음 두 가지 방법을 지원합니다.

* **SAML 발급자 접근 방식.**  이 접근법에서 &quot;요청자 ID&quot;는 SAML 인증 요청의 SAML 발급자 문자열에 추가됩니다.

* **사용자 지정 범위 지정 속성 접근 방식입니다.**  이 접근법에서 &quot;요청자 ID&quot;는 SAML 인증 요청에서 사용자 지정 &quot;범위 지정&quot; 속성으로 명시적으로 포함됩니다.

>[!NOTE]
>
>요청자 ID는 Adobe Primetime 인증이 프로그래머의 네트워크 브랜드를 참조하는 방법입니다(예: &quot;CNN&quot;은 터너 네트워크의 브랜드 중 하나이다.

### SAML 발급자 접근 방식 {#saml-issuer-approach}

이 접근법은 SAML을 사용합니다 `<Issuer>` 이 코드 조각에 표시된 대로 SAML 인증 요청의 요소:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 사용자 지정 범위 속성 접근 방법 {#custom-scoping-property-approach}

이 접근 방법에서는 SAML 인증 요청의 이 코드 조각에 표시된 대로 &quot;범위 지정&quot;이라는 사용자 지정 속성을 사용합니다.

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->