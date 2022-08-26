---
title: 인증 토큰 검색
description: 인증 토큰 검색
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# 인증 토큰 검색 {#retrieve-authorization-token}

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

인증(AuthZ) 토큰을 검색합니다.  


| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authz</br></br>예:</br></br>&lt;sp_fqdn>/api/v1/tokens/authz | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(필수)</br>2.  deviceId(필수)</br>3.  자원(필수)</br>4.  device_info/X-Device-Info(필수)</br>5.  _deviceType_</br> 6.  _deviceUser_ (더 이상 사용되지 않음)</br>7.  _appId_ (더 이상 사용되지 않음) | GET | 1. 성공</br>2.  인증 토큰  </br>    찾을 수 없거나 만료되지 않음:   </br>    이유를 설명하는 XML  </br>    인증 토큰이 없습니다.</br>3.  인증 토큰  </br>    찾을 수 없음:  </br>    XML 설명</br>4.  인증 토큰  </br>    만료:  </br>    XML 설명 | 200 - 성공  </br>412 - AuthN 없음</br></br>404 - AuthZ 없음</br></br>410 - AuthZ 만료됨 |

{style=&quot;table-layout:auto&quot;}

</br>

| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| 리소스 | resourceId(또는 MRSS 조각)를 포함하는 문자열로서, 사용자가 요청한 컨텐츠를 식별하고 MVPD 인증 끝점에 의해 인식됩니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br>자세한 내용은 [장치 및 연결 정보 전달](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. |

{style=&quot;table-layout:auto&quot;}


### 샘플 응답 {#response}

 

#### 성공

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
        <expires>1348148289000</expires>
        <mvpd>sampleMvpdId</mvpd>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <proxyMvpd>sampleProxyMvpdId</proxyMvpd>
    </authorization>
```

 

**JSON:**

```JSON
    {
        "mvpd": "sampleMvpdId",
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348148289000",
        "proxyMvpd": "sampleProxyMvpdId"
    }
```

 </br>


#### 인증 토큰이 없거나 만료되었습니다.

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>412</status>
        <message>User not authenticated</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 412,
        "message": "User not authenticated",
        "details": null
    }
```

</br>
 

#### 인증 토큰을 찾을 수 없습니다.

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found",
        "details": null
    }
```

</br>

 

#### 인증 토큰이 만료되었습니다.

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>410</status>
        <message>Gone</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 410,
        "message": "Gone",
        "details": null
    }
```

[Clientless API 참조로 돌아가기](http://tve.helpdocsonline.com/clientless-api-reference)
