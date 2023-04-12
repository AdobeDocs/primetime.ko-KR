---
title: MVPD 인증
description: MVPD 인증
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# MVPD 인증 {#mvpd-authn}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#mvpd-authn-overview}

실제 SP(서비스 공급자) 역할은 Programmer에서 보유하지만 Adobe Primetime 인증은 해당 Programmer의 SP 프록시 역할을 합니다. Adobe Primetime 인증을 매개체로 사용하면 MVPD와 프로그래머 모두 케이스별로 자격 부여 프로세스를 사용자 지정할 필요가 없습니다.

아래 단계는 프로그래머가 SAML을 지원하는 MVPD에서 인증을 요청할 때 Adobe Primetime 인증을 사용하여 이벤트 시퀀스를 제공합니다. Adobe Primetime 인증 Access Enabler 구성 요소는 사용자/가입자 클라이언트에서 활성화되어 있습니다. 여기서 Access Enabler는 인증 흐름을 모두 간편하게 처리합니다.

1. 사용자가 보호된 컨텐츠에 대한 액세스를 요청하면 Access Enabler가 Programmer(SP)를 대신하여 인증(AuthN)을 시작합니다.
1. SP의 앱에는 유료 TV 공급자(MVPD)를 얻기 위해 사용자에게 &quot;MVPD 선택기&quot;가 표시됩니다. 그러면 SP가 사용자의 브라우저를 선택한 MVPD의 ID 공급자(IdP) 서비스로 리디렉션합니다.  &quot;**프로그래머가 시작한 로그인**&quot;.  MVPD는 IdP의 응답을 Adobe의 SAML 어설션 소비자 서비스로 전송하며 여기서 처리합니다.
1. 마지막으로 Access Enabler는 브라우저를 다시 SP 사이트로 리디렉션하여 SP에 AuthN 요청의 상태(성공/실패)를 알려줍니다.

## 인증 요청 {#authn-req}

위의 단계에 설명된 대로 AuthN 흐름 중에 MVPD는 둘 다 SAML 기반 AuthN 요청을 수락하고 SAML AuthN 응답을 전송해야 합니다.

다음 [OLCA(Online Content Access) 인증 및 인증 인터페이스 사양](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} 는 표준 AuthN 요청 및 응답을 제공합니다. Adobe Primetime 인증에서는 MVPD가 이 표준을 기반으로 자격 메시지를 작성할 필요가 없지만 사양을 보면 AuthN 트랜잭션에 필요한 주요 속성에 대한 통찰력을 제공할 수 있습니다.

>[!NOTE]
>
>MVPD가 Adobe Primetime 인증을 사용하여 받는 AuthN 요청에는 디지털 서명이 포함되어 있습니다. 그러나 아래 예에는 간결성을 위해 서명이 표시되지 않습니다. 디지털 서명을 보여주는 예는 의 예를 참조하십시오. [인증 응답](#authn-response) 를 참조하십시오.

샘플 SAML 인증 요청:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

아래 표에서는 기본 예상 값과 함께 인증 요청에 있어야 하는 속성과 태그에 대해 설명합니다.

**SAML 인증 요청 세부 정보**

| samlp:AuthnRequest | &lt;authnrequest> 서비스 공급자가 ID 공급자에 발급했습니다. |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | 후속 응답에서 사용할 Adobe 끝점입니다. 기본값: **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| 대상 | 이 요청이 전송된 주소를 나타내는 URI 참조입니다. 이 기능은 일부 프로토콜 바인딩에 필요한 보호인 의도하지 않은 수신자에게 요청을 악성 전달하지 않도록 하는 데 유용합니다. 메시지가 있는 경우 실제 수신자는 URI 참조가 메시지를 받은 위치를 식별하는지 확인해야 합니다. 그렇지 않은 경우 요청을 삭제해야 합니다. 일부 프로토콜 바인딩에서는 이 속성을 사용해야 할 수도 있습니다. |
| 강제 작성 | ForceAuthn 속성은 값이 true인 경우 ID 제공자가 기존 세션에 의존하지 않고 이 ID를 새로 설정해야 합니다. 기존 세션은 주도자와 함께 사용할 수 있습니다. |
| ID | 요청에 대한 식별자입니다. 자세한 내용은 [SAML 코어 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 섹션 1.3.4 을 참조하십시오. |
| IsPassive | 부울 값. &quot;true&quot;이면 ID 공급자 및 사용자 에이전트 자체가 요청자로부터 사용자 인터페이스를 눈에 띄게 제어하고 발표자와 눈에 띄는 방식으로 상호 작용하지 않아야 합니다. 값을 제공하지 않으면 기본값은 &quot;false&quot;입니다. |
| IssueInstant | 응답 문제의 시간 인스턴스입니다. 시간 값은 다음과 같이 UTC로 인코딩됩니다 [SAML 코어 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 섹션 1.3.3. |
| ProtocolBinding | 를 반환할 때 사용할 SAML 프로토콜 바인딩을 식별하는 URI 참조입니다 &lt;response> 메시지를 표시합니다. 자세한 내용은 [SAMLBind] 프로토콜 바인딩 및 이에 대해 정의된 URI 참조에 대한 자세한 정보. 기본값 : urn:oasis:이름:tc:SAML:2.0:bindings:HTTP-POST |
| 버전 | 이 요청의 버전입니다. |
| saml:발급자 | 응답 메시지를 생성한 엔터티를 식별합니다. (이 요소에 대한 자세한 내용은 SAML 코어 2.0-os 섹션 2.2.5 을 참조하십시오.) |
| ds:서명 | SAML 코어 2.0-os에서 섹션 5에 설명된 대로 검증에 대한 무결성을 보호하고 어설션의 발행자를 인증하는 XML 서명 |
| samlp:NameIDPolicy | 요청된 제목을 나타내는 데 사용할 이름 식별자에 대한 제한을 지정합니다. |
| AllowCreate | 요청을 수행하는 과정에서 ID 공급자가 주도자를 나타내는 새 식별자를 만들 수 있는지 여부를 나타내는 부울 값입니다. 기본값: true |
| 형식 | 이름 식별자 형식에 해당하는 URI 참조를 지정합니다. 기본값: urn:oasis:이름:tc:SAML:2.0:nameid-format:임시 Adobe 권장 사항: urn:oasis:이름:tc:SAML:2.0:nameid-format:영구적 |
| SPNameQualifier | 요청자가 아닌 서비스 공급자의 네임스페이스에 검증 주체의 식별자가 반환되거나 생성되도록 지정합니다(선택적). 기본값 : http://saml.sp.adobe.adobe.com |

## 인증 응답 {#authn-response}

인증 요청을 받고 처리한 MVPD가 이제 인증 응답을 보내야 합니다.

**샘플 SAML 인증 응답**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>
```


위의 샘플에서 Adobe SP는 Subject/NameId에서 사용자 ID를 가져오기로 합니다. 사용자 정의 속성에서 사용자 ID를 가져오도록 Adobe SP를 구성할 수 있습니다. 응답에는 다음과 같은 요소가 포함되어야 합니다.

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**SAML 인증 응답 세부 정보**
| samlp:응답 | Adobe Primetime 인증에서 받은 응답입니다.                                                                                                                                                                                                                                                                                                                                                                                                                       | |—|—| | 대상 | 이 요청이 전송된 주소를 나타내는 URI 참조입니다. 이 기능은 일부 프로토콜 바인딩에 필요한 보호인 의도하지 않은 수신자에게 요청을 악성 전달하지 않도록 하는 데 유용합니다. 메시지가 있는 경우 실제 수신자는 URI 참조가 메시지를 받은 위치를 식별하는지 확인해야 합니다. 그렇지 않은 경우 요청을 삭제해야 합니다. 일부 프로토콜 바인딩에서는 이 속성을 사용해야 할 수도 있습니다. | | ID | 요청에 대한 식별자입니다. 이 유형은 xs:ID이며, 다음 섹션 1.3.4에 지정된 요구 사항을 따라야 합니다 [SAML 코어 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} 식별자 고유성. 요청에 있는 ID 속성 값과 해당 응답에 있는 InResponseTo 속성 값이 일치해야 합니다.                                                                                                                                                                                         | | InResponseTo | SAML 프로토콜 메시지의 ID로서, 인증 엔티티가 어설션을 제공할 수 있습니다. 값은 인증 요청에 전송된 ID 속성의 값과 같아야 합니다. SAML 코어 2.0-os 를 참조하십시오. | | IssueInstant | 요청 문제의 시간 인스턴스입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | 버전 | 요청의 버전입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml:발급자 | 요청 메시지를 생성한 엔터티를 식별합니다. (이 요소에 대한 자세한 내용은 섹션 2.2.5. SAML 코어 2.0-os 를 참조하십시오.) | | samlp:상태 | 해당 요청의 상태를 나타내는 코드입니다.                                                                                                                                                                                                                                                                                                                                                                                                               | | samlp:StatusCode | 해당 요청에 응답하여 수행된 활동의 상태를 나타내는 코드입니다.                                                                                                                                                                                                                                                                                                                                                                       | | saml:검증 | 이 유형은 모든 어설션에 공통되는 기본 정보를 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                        | | ID | 이 검증에 대한 식별자입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                         | | 버전 | 이 어설션의 버전입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                             | | IssueInstant | 요청 문제의 시간 인스턴스입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds:서명 | SAML Core 2.0-os에서 섹션 5에 설명된 대로 검증에 대한 무결성을 보호하고 발급자를 인증하는 XML 서명 | | ds:SignedInfo | SignedInfo 구조에는 정규화 알고리즘, 서명 알고리즘 및 하나 이상의 참조가 포함됩니다. SignedInfo 요소에는 다른 서명 및 개체에서 참조할 수 있는 선택적 ID 특성이 포함될 수 있습니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:CanonicalizationMethod | CanonicalizationMethod는 서명 계산을 수행하기 전에 SignedInfo 요소에 적용되는 정규화 알고리즘을 지정하는 필수 요소입니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:SignatureMethod | SignatureMethod는 서명 생성 및 유효성 검사에 사용되는 알고리즘을 지정하는 필수 요소입니다. 이 알고리즘은 서명 작업과 관련된 모든 암호화 기능(예: 해싱, 공개 키 알고리즘, MAC, 패딩 등)을 식별합니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:참조 | 참조는 하나 이상 발생할 수 있는 요소입니다. 다이제스트 알고리즘 및 다이제스트 값, 그리고 선택적으로 서명되는 객체의 식별자, 객체 유형 및/또는 다이제스트 전에 적용할 변형 목록을 지정합니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:변형 | 선택적 변형 요소에는 변형 요소의 순서가 지정된 목록이 포함되어 있습니다. 서명자가 소화된 데이터 개체를 획득하는 방법을 설명합니다. 각 변형의 출력은 다음 변형에 대한 입력으로 사용됩니다. 첫 번째 변형에 대한 입력은 참조 요소의 URI 속성을 역참조하는 결과입니다. 마지막 변형의 출력은 DigestMethod 알고리즘에 대한 입력입니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:DigestMethod | DigestMethod는 서명된 개체에 적용할 다이제스트 알고리즘을 식별하는 필수 요소입니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:DigestValue | DigestValue는 다이제스트의 인코딩된 값을 포함하는 요소입니다. 다이제스트는 항상 base64를 사용하여 인코딩됩니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:SignatureValue | SignatureValue 요소에 디지털 서명의 실제 값이 포함되어 있습니다. 항상 base64를 사용하여 인코딩됩니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:KeyInfo | KeyInfo는 수신자가 서명을 확인하는 데 필요한 키를 가져올 수 있도록 하는 선택적 요소입니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds:X509Data | KeyInfo 내의 X509Data 요소에 키 또는 X509 인증서의 식별자가 하나 이상 포함되어 있습니다. XML-서명 구문 및 처리 를 참조하십시오. | | ds: X509Certificate | base64로 인코딩된 X509C인증서 요소 [X509v3] 인증서 | | saml:제목 | 검증에 있는 문의 제목입니다.                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | &lt;nameid> 요소는 NameIDType 유형이며(SAML core 2.0-os에서 섹션 2.2.2 참조), &lt;subject> 및 &lt;subjectconfirmation> 및 를 포함할 수 없습니다.                                                                                                                                                                                                                                           | | 형식 | 문자열 기반 식별자 정보의 분류를 나타내는 URI 참조입니다.                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier | 서비스 공급자 이름 또는 공급자 소속 이름을 사용하여 이름을 추가로 정규화합니다. 이 속성은 신뢰 당사자 또는 당사자를 기반으로 이름을 페더레이션하는 추가 방법을 제공합니다.                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation | 대상을 확인할 수 있는 정보입니다. 주체 확인이 두 개 이상 제공되면, 해당 주체 중 어느 하나를 만족하면 해당 주장을 적용할 목적으로 해당 주제를 확인하기에 충분합니다.                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData | 특정 확인 방법으로 사용할 추가 확인 정보입니다. 예를 들어 이 요소의 일반적인 컨텐츠는 <!--<ds:KeyInfo>--> XML 서명 구문 및 처리 사양에 정의된 요소 | | NotOnOrAfter | 더 이상 대상을 확인할 수 없는 시간 인스턴스입니다.                                                                                                                                                                                                                                                                                                                                                                                                            | | 수신자 | 검증 엔티티가 어설션을 표시할 수 있는 엔티티 또는 위치를 지정하는 URI입니다. 예를 들어, 이 속성은 중계기가 다른 위치에서 이를 리디렉션하지 않도록 특정 네트워크 종단점에 검증이 전달되어야 함을 나타낼 수 있습니다.                                                                                                                                                                                   | | saml:조건 | &lt;condition> 요소는 새 조건에 대한 확장 포인트 역할을 합니다.                                                                                                                                                                                                                                                                                                                                                                                                   | | NotBefore | NotBefore 속성은 유효성 간격이 시작되는 시간 인스턴스를 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | &lt;audiencerestriction> 요소는 검증이 &lt;audience> 요소를 생성하지 않습니다.                                                                                                                                                                                                                                                                                                                           | | saml:대상 | 의도한 대상을 식별하는 URI 참조입니다.                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement | 인증 문.                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant | 인증이 발생한 시간을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                 | | SessionIndex | 주체가 식별한 주체와 인증 기관 간의 특정 세션 인덱스를 지정합니다.                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext | 이 문을 생성하는 인증 이벤트를 포함하여 인증 기관에서 사용하는 컨텍스트입니다.                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef | 다음에 오는 인증 컨텍스트 선언을 설명하는 인증 컨텍스트 클래스를 식별하는 URI 참조입니다. |