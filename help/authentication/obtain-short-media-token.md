---
title: 짧은 미디어 토큰 가져오기
description: 짧은 미디어 토큰 받기
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 짧은 미디어 토큰 가져오기 {#obtain-short-media-token}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## REST API 끝점 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 프로덕션 - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 스테이징 - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 스테이징 - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## 설명 {#description}

짧은 미디어 토큰을 가져옵니다.

| 엔드포인트 | 호출됨  </br>작성자: | 입력   </br>매개 변수 | HTTP  </br>방법 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediatoken</br></br>  또는</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>예:</br></br>&lt;sp_fqdn>/api/v1/tokens/media | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(필수)</br>2.  deviceId(필수)</br>3.  리소스(필수)</br>4.  device_info/X-Device-Info (필수)</br>5.  _deviceType_</br> 6.  _deviceUser_ (사용하지 않음)</br>7.  _appId_ (사용하지 않음) | GET | 실패한 경우 Base64로 인코딩된 미디어 토큰 또는 오류 세부 정보가 포함된 XML 또는 JSON입니다. | 200 - 성공  </br>403 - 성공 없음 |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 Programmer requestorId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| 리소스 | resourceId(또는 MRSS 조각)가 포함된 문자열은 사용자가 요청한 콘텐츠를 식별하며 MVPD 인증 종단점에서 인식됩니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보입니다.</br></br>**참고**: URL 매개 변수로 device_info를 전달할 수 있지만, 이 매개 변수의 잠재적 크기와 GET URL 길이 제한으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br>의 전체 세부 정보 보기 [전달 장치 및 연결 정보](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | 디바이스 유형(예: Roku, PC).</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음과 같은 지표를 제공합니다. [장치 유형별 분류]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) - Clientless를 사용할 때 다양한 유형의 분석을 수행할 수 있습니다. 예를 들어 Roku, AppleTV 및 Xbox가 있습니다.</br></br>다음을 참조하십시오 [Clientless devicetype 매개 변수 사용의 이점&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자.</br></br>**참고**: 사용하는 경우 deviceUser는 [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info가 이 매개 변수를 대체합니다. 사용하는 경우 `appId` 은(는) 과(와) 동일한 값을 가져야 합니다. [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |

{style="table-layout:auto"}

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



### Media Verification Library 호환성

필드 `serializedToken` &quot;짧은 미디어 토큰 얻기&quot; 호출에서 Adobe Medium 확인 라이브러리에 대해 확인할 수 있는 Base64로 인코딩된 토큰이 반환됩니다.
