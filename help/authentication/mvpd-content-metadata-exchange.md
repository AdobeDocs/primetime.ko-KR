---
title: MVPD 콘텐츠 메타데이터 교환
description: MVPD 콘텐츠 메타데이터 교환
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# MVPD 콘텐츠 메타데이터 교환

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#content-metadat-exchange-overview}

이 페이지에서는 Adobe Primetime 인증이 인증 요청 시 MVPD에게 구조화된 데이터를 전송하는 데 사용하는 두 가지 표준 구현에 대해 설명합니다.  구조화된 데이터는 요청을 수행하는 리소스(프로그래머)를 나타내고, 컨텐츠 등급과 같은 추가 데이터를 나타냅니다.

프로그래머 측에서 Adobe Primetime 인증은 다음과 같이 구조화된 MRSS 데이터 리소스를 지원합니다.

1. 프로그래머는 리소스를 MRSS 문자열로 전송합니다. Adobe Primetime 인증은 웹 또는 기본 장치용으로 클라이언트 측에서 인코딩하지 않습니다. MRSS는 Adobe Primetime 인증 서버에 일반 문자열로 전송됩니다.
1. 서버 측에서, MRSS는 사전 정의된 스키마(http://search.yahoo.com/mrss/)에 대해 검증됩니다.  유효성 검사가 전달되면 Adobe Primetime 인증은 MRSS 필드에서 다음을 포함한 정보를 추출합니다.
   * 채널 제목
   * 항목 제목
   * 리소스 식별자
   * 등급 값 및 유형
1. MRSS에서 추출된 값은 MVPD에 전달되는 인증 요청을 작성하는 데 사용됩니다.

Adobe Primetime 인증에서는 MRSS를 MVPD에서 지원하는 형식으로 변환하기 위한 두 가지 방법을 지원합니다.

* **XACML**.  첫 번째 방법은 OLCA 표준에 부합합니다.  MRSS 값이 추출되는 XACML을 사용하여 MRSS 요소에 매핑되는 특성을 사용하여 XACMLResource를 만듭니다.  그러면 MVPD에 전달됩니다.
* **REST**.  두 번째 방법은 REST 기반입니다.  MRSS는 base64로 인코딩되고 REST 호출 시 URL 매개 변수로 전달됩니다.

두 방법 모두에서 MVPD는 추출된 값을 자체 논리 흐름 내에 포함하고 인증 응답을 반환하여 인증 요청을 처리합니다.

## 통합 세부 사항 {#integration-details}

* OLCA 기반 XACML 구조화된 리소스
* REST 기반 구조화 리소스

### OLCA 기반 XACML 구조화된 리소스 {#olca-based-xacml-struc-resource}

대부분의 케이블 기반 MVPD는 XACML 기반 접근 방식을 사용하지만 아직 전체 구조화된 데이터 접근 방식은 지원하지 않습니다.  XACML을 지원하는 다른 MVPD는 채널 제목을 선택하고 ResourceID 특성에 대해 이를 수락합니다. 아래 예는 구조화된 XACML 기반 전체 접근 방식을 보여줍니다. Adobe Primetime 인증 팀에서는 XACML을 사용하지만 자녀 보호 등의 기능을 아직 지원하지 않는 MVPD의 경우 다음 예에 따라 XACML 통합을 조정해야 합니다.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### REST 기반 구조화 리소스 {#rest-based-struct-resource}

일부 MVPD는 다음 권한 부여에 대한 REST 기반 프로토콜에 대해 표준화했습니다. 이 접근 방식은 XACML 접근 방식과 마찬가지로 모든 기능을 갖추고 있지만 &quot;가중치&quot; 구현을 제공합니다.

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->