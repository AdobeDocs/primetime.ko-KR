---
title: 프리플라이트 권한 부여
description: 프리플라이트 권한 부여
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# 프리플라이트 권한 부여 {#preflight-authorization}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

## 개요 {#overview}

이 기능은 여러 리소스에 대한 간단한 인증 검사를 제공합니다. 이 간단한 확인의 목적은 UI를 장식하는 것입니다(예: 잠금 및 잠금 해제 아이콘으로 액세스 상태를 표시). 프리플라이트 권한 부여는 리소스 목록에 대한 권한 부여 상태를 단일 API 호출로 가져오므로 가능한 가볍고 효율적입니다. 리소스 인증과 관련하여 이 기능은 권한이 없습니다.

A `getAuthorization(resource)` 또는 `checkAuthorization(resource)` 재생을 허용하기 전에 여전히 MUST를 호출해야 합니다.

프리플라이트 권한 부여는 또한 다른 사용 사례를 지원합니다. 이 경우 프로그래머는 하나의 미디어 컨텐츠를 재생하기 위해 여러 리소스 ID에 대한 권한 부여를 요청해야 합니다. 프로그래머는 필요한 리소스에 대해 초기 프리플라이트 검사를 수행할 수 있으며, 응답에 따라 비즈니스 조건이 충족되지 않으면 일찍 실패할 수 있습니다.

프리플라이트 인증을 지원하는 MVPD 목록은 [MVPD 프리플라이트 인증](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) 페이지. 

>[!NOTE]
>
> 전체 프리플라이트 인증 지원이 없는 MVPD에 대한 이 기능의 사용은 Adobe 및 MVPD와 먼저 동의해야 합니다. 이러한 MVPD에 대한 프리플라이트 권한 부여의 사용은 다음과 같은 &quot;최악의 사례 시나리오&quot;에 속합니다 [여기](/help/authentication/mvpd-preflight-authz.md#intro) 이로 인해 성능 문제가 발생하고 응답 시간이 느려질 수 있습니다. </br>
> 또한 프리플라이트 권한 부여 사용 시 **Adobe이 5개 이상의 리소스를 명시적으로 동의해야 합니다**.

## AccessEnabler Preflight API {#AE_pre_api}

AccessEnabler는 프리플라이트 인증을 구현하기 위해 API/콜백 함수 쌍을 표시합니다. API 호출은 리소스 목록으로 구성된 단일 매개 변수를 사용합니다. 콜백 함수에서는 실제 승인된 리소스를 나타내는 단일 매개 변수를 사용합니다. 다음 예는 ActionScript에 있지만 모든 종류의 AccessEnabler에서 호출을 사용할 수 있습니다.

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

리소스 목록에 대한 인증 상태를 요청하려면 AccessEnabler 개체에서 이 함수를 호출합니다.

Resources 매개 변수는 인증을 확인해야 하는 리소스 목록입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 `getAuthorization()` 즉, Programmer와 MVPD 또는 미디어 RSS 조각 간에 설정된 값에 대해 동의됩니다. Adobe Primetime 인증은 MVPD가 실제로 지원하는 항목에 따라 리소스 형식을 변환할 수 있는 씬 조정 계층 외에는 어떤 식으로든 리소스를 관리하지 않습니다.

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

프로그래머의 상위 계층 애플리케이션에서 구현해야 하는 콜백 함수입니다. AccessEnabler는 인증된 리소스 목록을 계산한 후 이 함수를 호출합니다.


### JS 예

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## 구현 정보 {#details}

- [ChannelID를 사용하여 프리플라이트](#preflight_using_channelID)
- [POST/사전 인증](#post)
- [스토리지](#storage)

API 호출은 클라이언트의 로컬 저장소에서 현재 사용자에 대해 캐시된 인증된 리소스 목록을 찾습니다. 캐시된 목록이 없는 경우 목록을 검색하기 위해 AdobePass 서버에 HTTPS 호출이 수행됩니다.

캐싱 메커니즘은 네트워크 호출을 모두 건너뛰어서 후속 호출 시 성능 시간을 향상시킵니다. 또한, 상기 캐싱된 목록은 상기 인증 프로세스의 일부로 미리 채울 수 있다.  (이 시나리오 설정에 대한 자세한 내용은 [프리플라이트 인증 통합](/help/authentication/authz-usecase.md#preflight_authz_int) ( MVPD 통합 가이드의 인증 섹션).

또한, 캐시된 리소스 목록이 존재하는 경우, 해당 리소스 목록을 사용하여 승인 흐름을 최적화할 수 있습니다. `checkAuthorization()` 네트워크 호출을 수행하기 전에 확인할 수 있습니다. 리소스가 사전 승인된 리소스 목록에 없는 경우 Primetime 인증 서버를 호출하지 않아도 검사가 실패할 수 있습니다.


### ChannelID를 사용하여 프리플라이트 {#preflight_using_channelID}

Primetime 인증 2.4.1 릴리스부터 Preflight 흐름은 다음과 같이 작동합니다.

1. 인증 중에 Primetime 인증은 `channelIID` mvpd의 SAML 응답에서 요소를 가져온 후 이 값을 사용하여 `authorizedResources` 인증 토큰의 요소입니다.
1. 내부 `checkPreauthorizedResources()` API 함수, Primetime 인증은 `authorizedResources` 요소가 설정되어 있습니다.
1. 만약 `authorizedResources` 요소가 설정되면 Primetime 인증은 해당 값을 읽고 리소스 목록에서 교차 영역을 수행합니다 `authorizedResources` 요소 및 받는 리소스 목록 `checkPreauthorizedResources()` 매개 변수.  이 교차의 결과는 사전 승인된 리소스의 최종 목록입니다.
1. 만약 `authorizedResources` 요소가 설정되지 않은 경우 이전에 구현된 흐름을 실행합니다. 이 흐름에서 받은 리소스 목록이 사용됩니다 `checkPreauthorizedResources()` 매개 변수가 PreAuthorizationServlet에 전달됩니다. 이 서블릿은 MVPD 종단점에 대한 인증 호출을 수행하고 사전 승인된 리소스 목록을 반환합니다.

### ChannelID를 사용한 프리플라이트 예

아래 예는 샘플 채널 목록을 보여줍니다. 채널 목록을 전송하는 데 사용되는 특성의 이름은 한 MVPD와 다른 MVPD로 다를 수 있습니다.

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

다음 `authorizedResources` 인증 요소의 요소는 다음과 같이 표시됩니다.

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

프로그래머가 `checkPreauthorizedResources()` 다음 매개 변수 목록을 전달하는 API 호출:</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

현재 Preflight 구현에서는 `authorizedResources` 요소를 사용하여 이 목록을 반환합니다.

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**참고:** 교차 지점은 대/소문자를 구분하지 않습니다.

 

### POST/사전 인증 {#post}

이 호출은 캐시되고 인증된 리소스 목록이 없을 때 AccessEnabler에 의해 자동으로 수행됩니다. 


#### 요청 {#req}

| 매개 변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `authentication_token` | string | 예 | 인증 토큰. |
| `resource_id` | string | 예 | 단일 리소스. 에 제공된 리소스 배열의 각 요소에 대해 한 번에 여러 번 지정할 수 있습니다 `checkPreauthorizedResources()` API 호출. |


**참고:** 요청된 최대 리소스 수를 구성할 수 있습니다.
**최대 기본값은 5입니다.**


#### 응답 {#resp}

사전 인증 서블릿이 다시 보내는 응답에는 다음 형식이 있습니다.

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### 스토리지 {#storage}

AccessEnabler가 서비스 공급자에서 가져오는 사전 권한 리소스 목록입니다. 리소스 목록:

- AuthN 및 AuthZ 토큰과 함께 저장됩니다.
- 사용자가 동일한 웹 사이트에 있거나 AuthN 토큰이 만료될 때까지 유효합니다
- 사용자가 새로운 Primetime 인증 통합 웹 사이트에 도착할 때마다 다시 검색됩니다

각 항목에는 사용자가 사전 인증한 리소스 ID가 포함되어 있습니다.

예:


| 리소스 ID | 인증됨 |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


이 목록의 이름은 &quot;사전 인증 캐시&quot;입니다.

#### 흐름 {#flow}

1. 프로그래머의 앱/사이트가 `checkPreauthorizedResources(resourceList)` 호출.
1. AccessEnabler는 인증된 리소스에 대한 인증 토큰을 확인합니다.
   1. 인증 토큰에 인증된 리소스가 포함되어 있는 경우 - 이 목록은 권한이 있으므로 이 정보를 얻기 위해 호출을 수행할 필요가 없습니다. resourceList의 리소스는 인증 토큰의 인증된 리소스 목록 내에서 검색되며 찾은 리소스만 `preauthorizedResources()` 콜백입니다.
   1. 인증 토큰에 인증된 리소스가 포함되지 않은 경우 - `resourceList` 는 사전 인증 캐시의 리소스 목록과 비교됩니다.
      1. 목록에 동일한 리소스가 포함되어 있으면 이는 서버에 대한 호출이 이미 수행되었으며 응답이 이미 사전 인증 캐시에 있음을 의미합니다. 승인된 리소스만 `preauthorizedResources()` 콜백입니다.
      1. 목록에 동일한 리소스가 포함되어 있지 않은 경우, resourceList의 리소스에 대한 인증 상태를 가져오려면 클라이언트가 서버를 호출해야 합니다. 응답을 가져와 사전 인증 캐시에 저장하여 이전 리소스를 완전히 바꿉니다. 승인된 리소스만 `preauthorizedResources()` 콜백입니다.


#### 목록 검색 {#listRetrieve}

항상 `checkPreauthorizedResources()` 이 호출되면 권한 부여 캐시에 대해 권한 확인을 위한 리소스 목록이 확인됩니다. 목록에 동일한 리소스 세트가 포함되어 있으면 를 트리거하는 데 필요한 모든 리소스가 포함되므로 서비스 공급자를 호출하지 않습니다 `preauthorizedResources()` 콜백이 이미 캐시에 있습니다.


#### logout() {#logout}

로그아웃 시 사전 권한 부여 캐시가 비어 있습니다.


## 종속성 {#depends}

Preflight API의 성능은 특정 MVPD 구현에 따라 다릅니다.  구현 옵션에 대해서는 [프리플라이트 인증 통합](/help/authentication/authz-usecase.md#preflight_authz_int) ( MVPD 통합 가이드의 인증 섹션)을 참조하십시오.


## 보안 {#security}

모든 프로그래머가 클라이언트 API를 사용할 수 있습니다.

이 구현에서는 HTTPS를 전송으로 사용하지만, 더 가벼운 호출을 위해 추가 보안 정책이 사용되지 않습니다(서명 없음, FAX 없음).

**주의:** 보호된 리소스에 대한 액세스 권한을 사용자에게 부여해야 하는지 여부를 권한 있는 방법으로 이 API를 사용하지 마십시오. 이 API의 목적은 UI 장식 및/또는 사전 조명 비즈니스 의사 결정입니다. 다음 `getAuthorization()` 및 `checkAuthorization()` 는 항상 재생을 허용하기 전에 호출해야 합니다.


## 호환성 {#compat}

이 기능은 AccessEnabler의 모든 버전에서 지원됩니다. AS, JS, AIR, iOS, Android, Xbox (2번째 화면 AuthN 흐름).

프리플라이트 권한 부여는 CDATA 섹션이 포함된 사전 권한 부여 리소스를 지원하지 않습니다. 현재 프리플라이트 시스템의 초점은 채널 수준 필터링을 지원하는 것입니다. CDATA 섹션이 있는 리소스는 자산 수준 리소스입니다. 프리플라이트 기능은 `mrss` CDATA가 포함되지 않은 경우 채널 수준 사전 인증을 위한 리소스입니다. 

## 다른 기능과 통합 {#integ_w_other_features}

리소스가 사전 승인된 리소스 목록에 없는 경우, 권한 부여 플로우에서 가능한 최적화가 발생할 수 있습니다.

이 최적화를 통해 서버 프리플라이트 종단점은 Degration 메커니즘과 통합됩니다.  

MVPD 및 요청자에 대해 &quot;AuthN All&quot; 규칙이 있는 경우 프리플라이트 종단점은 요청에서 받은 모든 리소스를 미러링합니다.

요청에 있는 리소스 중 하나 이상에 대해 &quot;AuthZ All&quot;이 활성화된 경우에도 마찬가지입니다.

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
