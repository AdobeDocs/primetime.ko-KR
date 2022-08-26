---
title: 짧은 미디어 토큰 가져오기
description: 짧은 미디어 토큰 가져오기
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# 짧은 미디어 토큰 가져오기 {#obtain-short-media-token}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## REST API 엔드포인트 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 설명 {#description}

짧은 미디어 토큰을 가져옵니다.  

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediattoken</br></br>  또는</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>예:</br></br>&lt;sp_fqdn>/api/v1/tokens/media | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(필수)</br>2.  deviceId(필수)</br>3.  자원(필수)</br>4.  device_info/X-Device-Info(필수)</br>5.  _deviceType_</br> 6.  _deviceUser_ (더 이상 사용되지 않음)</br>7.  _appId_ (더 이상 사용되지 않음) | GET | Base64 인코딩 미디어 토큰 또는 실패한 경우 오류 세부 정보가 포함된 XML 또는 JSON입니다. | 200 - 성공  </br>403 - 성공 없음 |

{style=&quot;table-layout:auto&quot;}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| 리소스 | resourceId(또는 MRSS 조각)를 포함하는 문자열로서, 사용자가 요청한 컨텐츠를 식별하고 MVPD 인증 끝점에 의해 인식됩니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br>자세한 내용은 [장치 및 연결 정보 전달](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다.</br></br>**참고**: 를 사용하는 경우 deviceUser는 와 동일한 값을 가져야 합니다 [등록 코드 만들기](http://tve.helpdocsonline.com/registration-code-request) 요청. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. 사용하는 경우, `appId` 에는 와 동일한 값이 있어야 합니다. [등록 코드 만들기](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) 요청. |

{style=&quot;table-layout:auto&quot;}

### 샘플 응답 {#response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <play>
        <expires>1348649569000</expires>
        <mvpdId>sampleMvpdId</mvpdId>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <serializedToken>PHNpZ25hdH[...]</serializedToken>
        <userId>sampleScrambledUserId</userId>
    </play>
```



**JSON:**

```JSON
    {
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348649614000",
        "serializedToken": "PHNpZ25hdH[...]",
        "userId": "sampleScrambledUserId",
        "mvpdId": "sampleMvpdId"
    }
```

 

### 미디어 확인 라이브러리 호환성

필드 `serializedToken` &quot;짧은 미디어 토큰 가져오기&quot; 호출에서 는 Adobe Medium 확인 라이브러리에 대해 확인할 수 있는 Base64 인코딩 토큰입니다.

[REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
