---
title: MVPD 프리플라이트 인증
description: MVPD 프리플라이트 인증
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# MVPD 프리플라이트 인증

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#mvpd-preflight-authz-intro}

&quot;프리플라이트 권한 부여&quot;는 여러 리소스에 대한 간단한 권한 부여입니다. 프로그래머는 주로 UI를 장식하는 데 사용합니다(예: 잠금 및 잠금 해제 아이콘으로 액세스 상태를 표시).

Adobe Primetime 인증은 현재 AuthN 응답 속성을 통해 또는 다중 채널 AuthZ 요청을 통해 MVPD에 대해 두 가지 방법으로 프리플라이트 인증을 지원할 수 있습니다.  다음 시나리오에서는 프리플라이트 인증을 구현할 수 있는 다양한 방법의 비용/이점을 설명합니다.

* **최상의 사례 시나리오** - MVPD는 인증 단계(다중 채널 AuthZ) 동안 사전 승인된 리소스 목록을 제공합니다.
* **최악의 사례 시나리오** - MVPD가 여러 리소스 권한 부여를 지원하지 않는 경우 Adobe Primetime 인증 서버는 리소스 목록의 각 리소스에 대해 MVPD에 대한 권한 부여 호출을 수행합니다. 이 시나리오는 프리플라이트 인증 요청의 응답 시간에 영향을 줍니다(리소스 수에 비례함). 이렇게 하면 Adobe 및 MVPD 서버 모두에 대한 로드가 증가하여 성능 문제가 발생할 수 있습니다. 또한 재생이 실제로 필요하지 않은 승인 요청/응답 이벤트를 생성합니다.
* **사용되지 않음** - MVPD는 인증 단계 동안 사전 허가된 리소스 목록을 제공하므로 프리플라이트 요청도 필요하지 않으며, 목록이 클라이언트에 캐시되므로 네트워크 호출도 필요하지 않습니다.

MVPD는 프리플라이트 인증을 지원하지 않아도 되지만 다음 섹션에서는 Adobe Primetime 인증이 지원할 수 있는 몇 가지 프리플라이트 인증 방법에 대해 설명하면서 위의 최악의 사례 시나리오로 돌아갑니다.

## AuthN에서 프리플라이트 {#preflight-authn}

이 프리플라이트 시나리오는 OLCA 호환(Cableabs)입니다. &quot;인증 검증 내의 특성 문&quot;이라는 제목이 있는 인증 및 인증 인터페이스 1.0 사양 섹션 7.5.2는 SAML 인증 응답이 사전 승인된 리소스 목록을 포함할 수 있는 방법을 설명합니다. IdP가 이를 지원하는 경우 Adobe Primetime 인증 서버는 인증 시 미리 지정된 리소스 목록을 생성하고 인증 토큰과 함께 클라이언트에 캐시할 수 있습니다. 또한 이 메서드는 최상의 사례 시나리오를 수행하므로 Programmer가 checkPreauthorizedResources()를 호출하면 모든 항목이 이미 클라이언트에 있으므로 네트워크 호출이 수행되지 않습니다.

### SAML 특성 문의 사용자 지정 리소스 목록 {#custom-res-saml-attr}

IdP의 SAML 인증 응답에는 AdobePass에서 인증해야 하는 리소스 이름이 포함된 AttributeStatement가 포함되어야 합니다.  일부 MVPD는 다음 형식으로 제공합니다.

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

위의 샘플은 사전 승인된 두 리소스가 들어 있는 목록을 보여 줍니다. &quot;MMOD&quot; 및 &quot;올림픽 2012&quot;.

이렇게 하면 최상의 사례 시나리오를 효과적으로 수행할 수 있으며, 모든 항목이 이미 클라이언트에 있으므로 Programmer가 checkPreauthorizedResources()를 호출할 때 네트워크 호출이 수행되지 않습니다.

## AuthZ의 다중 채널 프리플라이트 {#preflight-multich-authz}

이 프리플라이트 구현은 OLCA 호환(Cabllabs)이기도 합니다.  인증 및 인증 인터페이스 1.0 사양(섹션 7.5.3 및 7.5.4)은 SAML 어설션 또는 XACML을 사용하여 MVPD에서 인증 정보를 요청하는 방법에 대해 설명합니다. 인증 흐름의 일부로 이 기능을 지원하지 않는 MVPD에 대한 인증 상태를 쿼리하는 데 권장되는 방법입니다. Adobe Primetime 인증에서는 인증된 리소스 목록을 검색하기 위해 MVPD에 대한 단일 네트워크 호출을 실행합니다.


Adobe Primetime 인증은 프로그래머 응용 프로그램에서 리소스 목록을 받습니다. 그런 다음 Adobe Primetime 인증의 MVPD 통합은 이러한 모든 리소스를 포함하는 하나의 AuthZ 호출을 수행한 다음 응답을 구문 분석하고 여러 허용/거부 결정을 추출할 수 있습니다.  다중 채널 AuthZ 시나리오가 있는 프리플라이트 흐름은 다음과 같이 작동합니다.

1. Profmer의 앱은 Preflight 클라이언트 API를 통해 쉼표로 구분된 리소스 목록을 보냅니다. 예를 들면 다음과 같습니다. &quot;TestChannel1,TestChannel2,TestChannel3&quot;
1. MVPD 프리플라이트 AuthZ 요청 호출에는 여러 리소스가 포함되어 있으며 다음 구조가 있습니다.

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## 여러 리소스에 대한 사용자 지정 인증 {#custom-authz}

일부 MVPD에는 한 요청에서 여러 리소스에 대한 인증을 지원하는 인증 종단점이 있지만 다중 채널 AuthZ에 설명된 시나리오에 해당되지 않습니다. 이러한 특정 MVPD에는 사용자 지정 작업이 필요합니다.

또한 Adobe은 기존 구현을 변경하지 않고 여러 채널 인증을 지원할 수 있습니다.  이 방법은 Adobe과 MVPD 기술 팀 간에 검토하여 예상대로 작동하는지 확인해야 합니다.

## 프리플라이트 인증을 지원하는 MVPD {#mvpds-supp-preflight-authz}

다음 표에는 프리플라이트 인증을 지원하는 MVPD와 프리플라이트 유형 및 알려진 제한 사항이 나와 있습니다.

| 프리플라이트 방식 | MVPD | 참고 |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| 다중 채널 AuthZ | Comcast AT&amp;T 프록시 Clearleap Charter_Direct 프록시 GLDS Verizon OSN Bell Sasktel Optimal AltimOne |  |
| 사용자 메타데이터의 채널 목록 | 갑자기 연결되는 HTC | 모든 Synacor 직접 통합도 이 방법을 지원할 수 있습니다. |
| 포크 및 가입 | 위에 나열되지 않은 다른 모든 항목 | 확인된 기본 최대 리소스 수는 5입니다. |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
