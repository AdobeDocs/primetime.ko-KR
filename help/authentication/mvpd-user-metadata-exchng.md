---
title: MVPD 사용자 메타데이터 교환
description: MVPD 사용자 메타데이터 교환
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# MVPD 사용자 메타데이터 교환

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#intro-user-metadata-exchange}

MVPD는 일부 경우에 프로그래머와 공유되는 고객에 대한 사용자별 메타데이터를 유지합니다. Adobe Primetime 인증의 목적은 이 &quot;사용자 메타데이터&quot;의 교환을 중개하는 것이지만 교환과 관련된 어떠한 종류의 규칙도 집행하지 않는 것입니다. 교환 규칙은 MVPD가 프로그래머 파트너와 함께 작업할 수 있도록 합니다.

exchange에 사용할 수 있는 사용자 메타데이터 유형에는 현재 다음 항목이 포함되어 있습니다.

* 우편 번호
* 최대 등급(VChip 또는 MPAA)
* 사용자 ID
* 가구 ID
* 채널 ID

이 기능을 사용하여 MVPD 및 프로그래머는 자녀 보호 등의 특수 사용 사례를 구현할 수 있습니다. 예를 들어, MVPD는 유해 컨텐츠 등급 데이터를 프로그래머에게 전달하면 이 데이터를 사용하여 사용자의 사용 가능한 보기 선택 사항을 필터링합니다.

사용자 메타데이터 주요 사항:

* MVPD는 인증 및 인증 흐름 중에 사용자 메타데이터를 프로그래머 애플리케이션에 전달합니다
* Adobe Primetime 인증에서는 AuthN 및 AuthZ 토큰에 메타데이터 값을 저장합니다
* Adobe Primetime 인증은 사용자 메타데이터를 다른 형식으로 제공하는 MVPD의 값을 정규화할 수 있습니다
* 일부 매개 변수는 프로그래머의 키를 사용하여 암호화할 수 있습니다
* 특정 값은 구성 변경을 통해 Adobe이 사용할 수 있습니다

>[!NOTE]
>
>사용자 메타데이터는 이전에 Adobe Primetime 인증에서 사용할 수 있었던 정적 메타데이터(인증 토큰 TTL, 인증 토큰 TTL 및 장치 ID)의 확장입니다.

## 예 {#example-mvpd-user-metadata-exch}

### 자녀 보호 {#example-parental-control}

이 예는 다음 항목을 보여줍니다.

* [프로그래머에서 MVPD 메타데이터 교환](#progr-mvpd-metadata-exch)

* [MVPD에서 프로그래머로 메타데이터 교환 흐름](#mvpd-progr-exchange-flow)

### 프로그래머에서 MVPD 메타데이터 교환 {#progr-mvpd-metadata-exch}

현재 Programmer API, Adobe Primetime 인증 및 MVPD Authorizer는 모두 채널 수준 인증만 지원합니다. 채널은 Programmer&#39;s getAuthorization() API 호출에서 일반 텍스트 문자열로 지정됩니다. 이 문자열은 MVPD의 인증 백엔드에 모든 방법으로 전파됩니다.

프로그래머의 앱 또는 사이트에서 사용자는 XACML 지원 MVPD(이 예에서는 &quot;TNT&quot;)를 선택합니다. XACML에 대한 자세한 내용은 [확장 가능한 액세스 제어 마크업 언어](https://en.wikipedia.org/wiki/XACML){target=_blank}.
프로그래머 앱은 리소스 및 해당 메타데이터를 포함하는 AuthZ 요청을 형성합니다.  이 예에는 채널 요소의 media 속성에 &quot;pg&quot;라는 MPAA 등급이 포함되어 있습니다.

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Adobe Primetime 인증은 MVPD와 프로그래머가 모두 지원하는 경우 자산 수준으로 더 세분화된 인증을 실제로 지원합니다. 리소스와 해당 메타데이터는 Adobe에 불투명합니다. 목적은 리소스 ID 및 메타데이터를 정규화된 방식으로 지정하여 리소스 ID를 다른 MVPD로 전송하기 위한 표준 형식을 설정하는 것입니다.

>[!NOTE]
>
>사용자가 채널 전용 지원 MVPD를 선택한 경우 Adobe Primetime 인증은 채널 제목(&quot;TNT&quot; )만 추출하고 MVPD에 제목만 전달합니다.

### MVPD에서 프로그래머로 메타데이터 교환 흐름 {#mvpd-progr-exchange-flow}

Adobe Primetime 인증은 다음과 같은 가정을 합니다.

* MVPD가 SAML 응답의 일부로 최대 등급을 전송합니다
* 이 정보는 인증 토큰의 일부로 저장됩니다
* API는 프로그래머가 이 정보를 검색할 수 있도록 Adobe Primetime 인증에서 제공합니다
* 프로그래머는 사이트 또는 앱에서 이 기능을 구현합니다(예를 들어 사용자의 최대 등급 이상인 비디오를 숨기기 위해)

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### 참고 {#notes-mvpd-progr-metadata-exch-flow}

**리소스 표준화 및 유효성 검사** 리소스 ID는 일반 문자열 또는 MRSS 문자열로 전달할 수 있습니다. 프로그래머는 일반 문자열 형식이나 MRSS를 사용할 수 있지만 MVPD가 해당 리소스를 처리하는 방법을 알 수 있도록 MVPD와 사전 계약이 필요합니다.

**리소스 ID 및 메타데이터 사양** Adobe Primetime 인증에서는 Media RSS 확장과 함께 RSS 표준을 사용하여 리소스 및 해당 메타데이터를 지정합니다. Media RSS 확장과 함께 Adobe Primetime 인증은 를 통해 보호자 통제 등의 다양한 메타데이터를 지원합니다 `<media:rating>`) 또는 geolocation ( )`<media:location>`).

Adobe Primetime 인증에서는 RSS가 필요한 MVPD에 대해 레거시 채널 문자열에서 해당 RSS 리소스로 투명한 전환을 지원할 수도 있습니다. 다른 방향에서 Adobe Primetime 인증은 채널 전용 MVPD에 대해 RSS+MRSS에서 일반 채널 제어로 변환을 지원합니다.

**Adobe Primetime 인증은 기존 통합과 완벽하게 호환됩니다.** 즉, 채널 수준 인증을 사용하는 프로그래머의 경우 Adobe Primetime 인증에서는 채널 ID를 해당 형식을 인식하는 MVPD로 보내기 전에 필요한 형식으로 패키지화하기 위해 처리합니다. 그 반대의 경우도 마찬가지입니다. 프로그래머가 모든 리소스를 새 형식으로 지정하는 경우 채널 수준 인증만 하는 MVPD에 대해 권한을 부여하는 경우 Adobe Primetime 인증은 새 형식을 단순 채널 문자열로 변환합니다.

## 사용자 메타데이터 사용 사례 {#user-metadata-use-cases}

더 많은 MVPD가 법적 준비를 하고 기능을 추가함에 따라 사용 사례는 계속 변경 및 확장되고 있습니다. 다음은 사용자 메타데이터를 사용할 수 있는 작업의 예입니다.

* [MVPD 사용자 ID](#mvpd-user-id)
* [가구 ID](#household-user-id)
* [우편 번호](#zip-code)
* [최대 등급(자녀 보호)](#max-rating-parental-control)
* [채널 목록](#channel-line-up)

### MVPD 사용자 ID {#mvpd-user-id}

* MVPD에서 제공한 대로
* MVPD가 해시하므로 사용자의 실제 로그인 정보가 아닙니다
* 을 사용하여 특정 사용자의 또는 문제를 나타낼 수 있습니다
* 암호화된
* MVPD 지원: 모든 MVPD

### 가구 사용자 ID {#household-user-id}

* 좋은 지표 정보를 허용합니다
* 암호화된
* MVPD 지원: 일부 MVPD

### 우편 번호 {#zip-code}

* 사용자의 청구 우편 번호입니다
* 주로 스포츠 이벤트 고정 기간 규칙을 적용하는 데 사용됩니다
* 빠른 업데이트에 대한 AuthZ 응답을 제공할 수 있습니다
* MVPD 지원: 일부 MVPD

### 최대 등급(자녀 보호) {#max-rating-parental-control}

* 처음에 AuthN 및 AuthZ 새로 고침
* UI에서 컨텐츠 필터링
* MPAA 또는 VChip 등급
* MVPD 지원: 일부 MVPD

### 채널 목록 {#channel-line-up}

* MVPD는 사용자가 볼 수 있는 채널 목록을 제공할 수 있습니다
* 빠른 UI 페인팅 허용
* OLCA 사양은 이를 AuthN 응답에서 AttributeStatement로 허용합니다
* MVPD 지원: 일부 MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
