---
title: 사전 인증
description: JavaScript 사전 인증
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# 사전 인증 {#js-preauthorize}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#preauth-overview}

API 사전 인증 방법은 애플리케이션에서 하나 이상의 리소스에 대한 사전 인증 결정을 가져오는 데 사용됩니다. API 사전 인증 요청은 UI 힌트 및/또는 콘텐츠 필터링에 사용해야 합니다. 사용자가 지정된 리소스에 액세스할 수 있도록 하려면 먼저 실제 인증 API 요청을 수행해야 합니다.

Adobe Primetime 인증 서비스에서 Preauthorization API 요청을 처리할 때 예기치 않은 오류(예: 네트워크 문제 및 MVPD 인증 끝점을 사용할 수 없음)가 발생하는 경우 API 사전 인증 응답 결과의 일부로 영향을 받는 리소스에 대해 하나 이상의 별도의 오류 정보가 포함됩니다.

### 공개 권한 부여(요청: PreauthorizationRequest, callback: AccessEnablerCallback&lt;any>): void {#preauth-method}

**설명:** 이 방법은 응용 프로그램에서 응용 프로그램의 UI를 장식하는 주요 목적(예: 잠금 및 잠금 해제 아이콘으로 액세스 상태를 표시)을 위해 특정 보호된 리소스를 보기 위해 Adobe Primetime 인증 서비스에서 인증된 사용자의 사전 인증(유용한) 결정을 얻는 데 사용됩니다.

**사용 가능:** v4.4.0+

**매개 변수:**

* `PreauthorizeRequest`: 요청을 정의하는 데 사용되는 빌더 개체
* `AccessEnablerCallback`: API 응답을 반환하는 데 사용되는 콜백
* `PreauthorizeResponse`: API 응답 콘텐츠를 반환하는 데 사용되는 개체

### class PreauthorizationRequestBuilder {#preath-req-builder-class}

#### setResources(리소스: string[]): PreauthorizationRequestBuilder {#set-res-preath-req-buildr}

* 사전 인증 결정을 얻을 리소스 목록을 설정합니다.
* 사전 인증 API를 사용하려면 반드시 설정해야 합니다.
* 목록의 각 요소는 리소스 ID 값을 나타내는 문자열이거나, MVPD와 동의해야 하는 미디어 RSS 조각을 나타내는 문자열이어야 합니다.
* 이 메서드는 현재 컨텍스트에서만 정보를 설정합니다 `PreauthorizeRequestBuilder` 이 메서드 호출의 수신자인 개체 인스턴스.

* 실제 `PreauthorizeRequest` 한번 보세요 `PreauthorizeRequestBuilder`&#39;s 메서드:

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` 리소스 를 참조하십시오. 사전 인증 결정을 얻을 리소스 목록입니다.
* `@returns {PreauthorizeRequestBuilder}` 동일한 항목에 대한 참조 `PreauthorizeRequestBuilder` 메서드 호출의 수신자인 개체 인스턴스.
* 이렇게 하면 메서드 체인을 만들 수 있습니다.

#### disableFeatures(...기능: string[]): PreauthorizationRequestBuilder {#disabl-featres-preauth-req-buildr}

* 사전 인증 결정을 가져올 때 비활성화할 기능을 설정합니다.
* 이 함수는 현재 컨텍스트에서만 정보를 설정합니다 `PreauthorizeRequestBuilder` 이 함수 호출의 수신자인 개체 인스턴스.
* 실제 `PreauthorizeRequest` 한번 보세요 `PreauthorizeRequestBuilder`의 함수:

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` 기능. 기능을 비활성화할 기능 세트입니다.
* `@returns` 동일한 항목에 대한 참조 `PreauthorizeRequestBuilder` 함수 호출 수신자인 개체 인스턴스.
* 함수 체인을 만들 수 있도록 이렇게 합니다.

#### build(): PreauthorizationRequest {#preauth-req}

* 새 `PreauthorizeRequest` 개체 인스턴스.
* 이 메서드는 `PreauthorizeRequest` 개체를 호출할 때마다 검색합니다.
* 이 메서드는 현재 컨텍스트에서 미리 설정된 값을 사용합니다 `PreauthorizeRequestBuilder` 이 메서드 호출의 수신자인 개체 인스턴스.
* 이 방법은 어떤 부작용도 발생하지 않는다는 점을 명심하십시오.
* 따라서 SDK의 상태나 페이지의 상태는 변경되지 않습니다 `PreauthorizeRequestBuilder` 이 메서드 호출의 수신자인 개체 인스턴스.
* 즉, 동일한 수신자에 대해 이 메서드를 연속적으로 호출하면 다른 새로운 메서드가 생성됩니다 `PreauthorizeRequest` 값이 `PreauthorizeRequestBuilder` 여기서 는 호출 간에 수정되지 않습니다.
* 제공된 정보(리소스 및 캐싱)를 업데이트할 필요가 없는 경우, 사전 권한 API의 여러 용도로 PreauthorizationRequest 인스턴스를 다시 사용할 수 있습니다.
* `@returns {PreauthorizeRequest}`

### 인터페이스 AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(result: T. {#on-response-result}

* 사전 권한 API 요청이 수행된 경우 SDK에서 호출하는 응답 콜백입니다.
* 결과는 성공했거나 상태를 포함하는 오류 결과입니다.
* `@param {T} result`

#### onFailure(result: T. {#on-failure-result}

* 사전 권한 API 요청을 처리할 수 없을 때 SDK에서 호출하는 실패 콜백입니다.
* 결과는 상태를 포함하는 실패 결과입니다.
* `@param {T} result`

### class PreauthorizationResponse {#preauth-response-class}

#### 공개 상태: 상태; {#public-status}

* 반환: 실패 시 추가 상태 정보.
* 다음을 보유할 수 있습니다. `null` 값.

#### 공개 결정: 결정[]; {#public-decisions}

* 반환: 사전 인증 결정 목록입니다. 각 리소스에 대해 하나의 결정.
* 실패 시 목록이 비어 있을 수 있습니다.

### 클래스 상태 {#class-status}

#### 공개 상태: number; {#public-status-numbr}

* RFC 7231에 설명된 대로 HTTP 응답 상태 코드입니다.
* 의 경우 0일 수 있습니다. `Status` 은 Adobe Primetime 인증 서비스 대신 SDK에서 가져옵니다.

#### 공개 코드: number; {#public-code-numbr}

* 표준 Adobe Primetime 인증 서비스 오류 코드입니다.
* 빈 문자열 또는 `null` 값.

#### 공개 메시지: string; {#public-msg-string}

* 경우에 따라 MVPD 인증 종단점 또는 프로그래머 성능 저하 규칙에 의해 제공되는 자세한 메시지입니다.
* 빈 문자열 또는 `null` 값.

#### 공개 세부 정보: string; {#public-details-strng}

* MVPD 인증 종단점 또는 Programmer 성능 저하 규칙에 의해 제공되는 자세한 메시지를 보관합니다.
* 빈 문자열 또는 `null` 값.


#### 공용 helpUrl: string; {#public-help-url-string}

* 이 상태/오류가 발생한 이유와 가능한 솔루션에 대한 자세한 정보를 연결하는 URL입니다.
* 빈 문자열 또는 `null` 값.

#### 공용 추적: string; {#public-trace-string}

* 보다 복잡한 시나리오에서 특정 문제를 식별하기 위해 지원에 문의할 때 사용할 수 있는 이 응답에 대한 고유 식별자입니다.
* 빈 문자열 또는 `null` 값.

#### 공개 작업: string; {#public-action-string}

* 상황을 수정할 권장 작업입니다.
   * **없음**: 안타깝게도 이 문제를 해결할 사전 정의된 작업이 없습니다. 이는 공용 API의 부적절한 호출을 나타낼 수 있습니다
   * **구성**: TVE 대시보드를 통해 또는 지원 팀에 연락하여 구성을 변경해야 합니다.
   * **애플리케이션 등록**: 신청서가 다시 등록되어야 한다.
   * **인증**: 사용자는 인증하거나 다시 인증해야 합니다.
   * **권한**: 사용자는 특정 리소스에 대한 인증을 받아야 합니다.
   * **분해**: 어떤 형태의 열화를 적용해야 합니다.
   * **다시 시도**: 요청을 재시도하면 문제가 해결될 수 있습니다
   * **다시 시도 후**: 표시된 기간이 문제를 해결할 수 있는 후 요청을 재시도합니다.
* 빈 문자열 또는 `null` 값.

### 클래스 결정 {#class-decision}

#### 공개 id: string; {#public-id-string}

* 결정을 얻은 리소스 ID입니다.

#### 공개 권한: 부울; {#public-auth-boolean}

* 결정이 성공했는지 여부를 나타내는 플래그 값입니다.

#### 공용 오류: 상태; {#public-error-status}

* 오류가 발생한 경우 추가 상태(상태) 정보입니다. 다음을 보유할 수 있습니다. `null` 값.

## 클라이언트 구현 예 {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## 시나리오 예 {#scenario-examples}

### 시나리오 1: 요청된 모든 리소스가 인증되었습니다. {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>비활성화됨</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### 시나리오 2: 요청된 리소스 중 일부가 승인되었습니다. {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>비활성화됨</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;결정&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>활성화됨</td>
    <td>

    &quot;JavaScript
    {
    &quot;결정&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;MVPD가 지정된 리소스에 대한 사전 인증을 요청할 때 \&quot;거부\&quot; 결정을 반환했습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 시나리오 3: 요청된 리소스 중 어느 것도 승인되지 않았습니다. {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>비활성화됨</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;결정&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>활성화됨</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;결정&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;MVPD가 지정된 리소스에 대한 사전 인증을 요청할 때 \&quot;거부\&quot; 결정을 반환했습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;MVPD가 지정된 리소스에 대한 사전 인증을 요청할 때 \&quot;거부\&quot; 결정을 반환했습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;maximum_execution_time_exceeded&quot;,
    &quot;message&quot;: &quot;요청이 최대 허용 시간 내에 완료되지 않았습니다. 요청을 재시도하면 문제가 해결될 수 있습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 시나리오 4: 잘못된 클라이언트 요청 - 지정된 리소스가 없습니다. {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>비활성화/활성화</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 400,
    &quot;code&quot;: &quot;internal_error&quot;,
    &quot;message&quot;: &quot;내부 오류로 인해 요청이 실패했습니다.&quot;
    &quot;details&quot;: &quot;필수 문자열[] 매개 변수 &#39;resource&#39;가 없습니다.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;결정&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 시나리오 5: 잘못된 클라이언트 요청 - 빈 리소스가 지정되었습니다. {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>비활성화/활성화</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 412,
    &quot;code&quot;: &quot;missing_resource&quot;,
    &quot;message&quot;: &quot;리소스 매개 변수가 없습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;결정&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 시나리오 6: 네트워크 오류입니다. {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>활성화됨</td>
    <td>

    &quot;JavaScript
    {
    &quot;결정&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;message&quot;: &quot;연결된 파트너 서비스에서 응답을 검색하는 동안 읽기 오류가 발생했습니다. 요청을 재시도하면 문제가 해결될 수 있습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;message&quot;: &quot;연결된 파트너 서비스에서 응답을 검색하는 동안 읽기 오류가 발생했습니다. 요청을 재시도하면 문제가 해결될 수 있습니다.&quot;
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 시나리오 7: 올바른 AuthN 세션 없이 사전 인증 흐름이 호출되었습니다.

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>비활성화/활성화</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;authentication_session_missing&quot;,
    &quot;message&quot;: &quot;이 요청과 연결된 인증 세션을 검색할 수 없습니다. 계속하려면 지원되는 MVPD로 다시 인증해야 합니다.&quot;,
    &quot;action&quot;: &quot;authentication&quot;
    },
    &quot;결정&quot;: []
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### 시나리오 8: setRequestor 호출이 완료되기 전에 미리 인증 흐름이 호출되었습니다.

<table>
<thead>
  <tr>
    <th>향상된 오류 코드 플래그</th>
    <th>응답</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>비활성화/활성화</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;requestor_not_configured&quot;,
    &quot;message&quot;: &quot;요청자가 setRequestor API 외에 API를 사용하기 위한 필수 구성 요소인 아직 구성되지 않았습니다.&quot;
    &quot;action&quot;: &quot;retry&quot;
    },
    &quot;결정&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

