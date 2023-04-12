---
title: 동적 클라이언트 등록 API
description: 동적 클라이언트 등록 API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# 동적 클라이언트 등록 API {#dynamic-client-registration-api}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#overview}

현재 Primetime 인증에서는 두 가지 방법으로 애플리케이션을 식별하고 등록합니다.

* 브라우저 기반 클라이언트는 를 통해 등록됩니다 [도메인 목록](/help/authentication/programmer-overview.md)
* iOS 및 Android 애플리케이션과 같은 기본 애플리케이션 클라이언트는 서명된 요청자 메커니즘을 통해 등록됩니다.

Adobe Primetime 인증에서는 애플리케이션을 등록하는 새 메커니즘을 제안합니다. 이 메커니즘은 다음 단락에 설명되어 있습니다.

## 응용 프로그램 등록 메커니즘 {#appRegistrationMechanism}

### 기술적 이유 {#reasons}

Adobe Primetime 인증의 인증 메커니즘은 세션 쿠키에 의존하지만 [Android Chrome 사용자 지정 탭](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}하지만 이 목표는 더 이상 달성될 수 없습니다.

Adobe은 이러한 제한 사항을 통해 모든 클라이언트를 위한 새로운 등록 메커니즘을 도입합니다. OAuth 2.0 RFC를 기반으로 하며 다음 단계로 구성됩니다.

1. TVE 대시보드에서 소프트웨어 문 검색
1. 클라이언트 자격 증명을 가져오는 중
1. 액세스 토큰 가져오기

### TVE 대시보드에서 소프트웨어 문 검색 {#softwareStatement}

릴리스할 각 응용 프로그램에 대해 소프트웨어 명세서를 받아야 합니다. 애플리케이션이 만들어지면 TVE 대시보드를 통해 모든 소프트웨어 구문을 제공합니다. 소프트웨어 문은 사용자의 장치에 있는 애플리케이션과 함께 배포되어야 합니다.

>[!IMPORTANT]
>
>소프트웨어 구문을 사용할 때 서명된 요청자 ID 메커니즘이 더 이상 필요하지 않습니다.

소프트웨어 구문을 만드는 방법에 대한 자세한 내용은 [TVE 대시보드의 클라이언트 등록](/help/authentication/dynamic-client-registration.md).

### 클라이언트 자격 증명을 가져오는 중 {#clientCredentials}

TVE Dashboard에서 소프트웨어 구문을 검색한 후 Adobe Primetime 인증 서버에 애플리케이션을 등록해야 합니다. /register 호출을 수행하고 고유한 클라이언트 식별자를 검색하여 이렇게 합니다.

**요청**

| HTTP 호출 |  |
|-----------|--------------------|
| 경로 | /o/client/register |
| 메서드 | POST |

| 필드 |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | TVE 대시보드에서 작성된 소프트웨어 문입니다. | 필수 |
| redirect_uri | 응용 프로그램이 인증 흐름을 완료하는 데 사용하는 URI입니다. | 옵션 |

| 요청 헤더 |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| 컨텐츠 유형 | application/json | 필수 |
| X-Device-Info | 전달 장치 및 연결 정보에 정의된 장치 정보 | 필수 |
| User-Agent | 사용자 에이전트 | 필수 |

**응답**

| 응답 헤더 |  |  |
|------------------|------------------|-----------|
| 컨텐츠 유형 | application/json | 필수 |

| 응답 필드 |  |  |
|---------------------|-----------------|----------------------------|
| client_id | 문자열 | 필수 |
| client_secret | 문자열 | 필수 |
| client_id_issued_at | 장기간 | 필수 |
| redirect_url | 문자열 목록 | 필수 |
| grant_types | 문자열 목록<br/> **허용 값**<br/> `client_credentials`: Android SDK와 같은 비보안 클라이언트가 사용합니다. | 필수 |
| 오류 | **허용된 값**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul> | 오류 플로우에서 필수입니다. |


#### 오류 응답 {#error-response}

오류가 발생하면 등록 서버가 HTTP 400(잘못된 요청) 상태 코드에 응답하고 응답 내에 다음 매개 변수를 포함합니다.

| 상태 코드 | 반응 본문 | 설명 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;: &quot;invalid_request&quot;} | 요청에 필수 매개 변수가 없거나, 지원되지 않는 매개 변수 값이 포함되어 있거나, 매개 변수를 반복하거나, 그렇지 않으면 형식이 잘못되었습니다. |
| HTTP 400 | {&quot;error&quot;: &quot;invalid_redirect_uri&quot;} | 등록된 응용 프로그램을 기준으로 이 클라이언트에 redirect_uri가 허용되지 않습니다. |
| HTTP 400 | {&quot;error&quot;: &quot;invalid_software_statement&quot;} | 소프트웨어 문이 잘못되었습니다. |
| HTTP 400 | {&quot;error&quot;: &quot;unapproved_software_statement&quot;} | software_id가 구성에 없습니다. |

#### 클라이언트 자격 증명 예 {#client-credentials-example}

**요청:**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**응답:**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**오류 응답:**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### 액세스 토큰 가져오기 {#accessToken}

애플리케이션에 대한 고유 클라이언트 식별자(클라이언트 ID 및 클라이언트 암호)를 검색한 후에는 액세스 토큰을 가져와야 합니다. 액세스 토큰은 Primetime 인증 API를 호출하는 데 사용되는 필수 OAuth 2.0 토큰입니다.

>[!NOTE]
>
>현재 액세스 토큰은 24시간 동안 사용할 수 있습니다.

**요청**


| **HTTP 호출** |  |
| --- | --- |
| 경로 | `/o/client/token` |
| 메서드 | POST |

| **요청 매개 변수** |  |
| --- | --- |
| `grant_type` | 클라이언트 등록 프로세스에서 수신되었습니다.<br/> **수락된 값**<br/>`client_credentials`: Android SDK와 같은 비보안 클라이언트에 사용됩니다. |
| `client_id` | 클라이언트 등록 프로세스에서 가져온 클라이언트 식별자입니다. |
| `client_secret` | 클라이언트 등록 프로세스에서 가져온 클라이언트 식별자입니다. |

**응답**

| 응답 필드 |  |  |
| --- | --- | --- |
| `access_token` | Primetime API를 호출하는 데 사용해야 하는 액세스 토큰 값 | 필수 |
| `expires_in` | access_token 이 만료될 때까지 남은 시간(초) | 필수 |
| `token_type` | 토큰의 유형 **bearer** | 필수 |
| `created_at` | 토큰의 문제 시간 | 필수 |
| **응답 헤더** |  |  |
| `Content-Type` | application/json | 필수 |

**오류 응답**

오류가 발생하면 인증 서버가 HTTP 400(잘못된 요청) 상태 코드에 응답하고 응답 내에 다음 매개 변수를 포함합니다.

| 상태 코드 | 반응 본문 | 설명 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;: &quot;invalid_request&quot;} | 요청에 필요한 매개 변수가 없거나, 지원되지 않는 매개 변수 값(그랜트 유형 제외)이 포함되어 있거나, 매개 변수를 반복하거나, 여러 자격 증명을 포함하거나, 클라이언트를 인증하기 위해 두 개 이상의 메커니즘을 사용하거나, 그렇지 않은 경우 형식이 잘못되었습니다. |
| HTTP 400 | {&quot;error&quot;: &quot;invalid_client&quot;} | 클라이언트를 알 수 없어서 클라이언트 인증에 실패했습니다. SDK는 인증 서버에 다시 등록해야 합니다. |
| HTTP 400 | {&quot;error&quot;: &quot;unauthorized_client&quot;} | 인증된 클라이언트가 이 권한 부여 형식을 사용할 수 있는 권한이 없습니다. |

#### 액세스 토큰 가져오기 예: {#obt-access-token}

**요청:**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**응답:**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**오류 응답:**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## 인증 요청 수행 {#autheticationRequests}

액세스 토큰을 사용하여 Adobe Primetime을 수행합니다 [인증 API 호출](/help/authentication/initiate-authentication.md). 이렇게 하려면 다음 방법 중 하나로 액세스 토큰을 API 요청에 추가해야 합니다.

* 요청에 새 쿼리 매개 변수를 추가하여 이 새 매개 변수를 라고 합니다 **access_token**.

* 새 HTTP 헤더를 요청에 추가하여 다음을 수행합니다. 권한 부여: 베어러 쿼리 문자열이 서버 로그에 표시되는 경향이 있으므로 HTTP 헤더를 사용하는 것이 좋습니다.

오류가 발생하면 다음 오류 응답이 반환될 수 있습니다.

| 오류 응답 |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | 요청의 형식이 잘못되었습니다. |
| invalid_client | 403 | 클라이언트 ID는 더 이상 요청을 수행할 수 없습니다. 새 클라이언트 자격 증명을 생성해야 합니다. |
| access_denied | 401 | access_token이 잘못되었습니다(만료되었거나 잘못되었습니다.). 클라이언트가 새 access_token을 요청해야 합니다. |

### 인증 요청 수행 예:

**액세스 토큰을 요청 매개 변수로 보내는 중:**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**액세스 토큰을 HTTP 헤더로 보내는 중:**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**응답 본문으로 오류 응답:**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**URL 매개 변수로서의 오류 응답:**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
