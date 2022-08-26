---
title: 두 번째 화면 웹 앱으로 사전 승인된 리소스 목록 검색
description: 두 번째 화면 웹 앱으로 사전 승인된 리소스 목록 검색
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 두 번째 화면 웹 앱으로 사전 승인된 리소스 목록 검색 {#retrieve-list-of-preauthorized-resources-by-second-screen-web-app}

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

사전 승인된 리소스 목록을 획득하기 위한 Adobe Primetime 인증 요청.

다음 두 가지 API 세트가 있습니다. 스트리밍 앱 또는 프로그래머 서비스용 세트와 두 번째 화면 웹 앱용 세트 1개. 이 페이지에서는 AuthN 앱에 대한 API에 대해 설명합니다.

 \
| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 | | — | — | — | — | — | — | | &lt;sp_fqdn>/api/v1/preauthorization/{registration code} | AuthN 모듈 | 1.  등록 코드  </br>    (경로 구성 요소)</br>2.  요청자(필수)</br>3.  리소스 목록(필수) | GET | 개별 사전 인증 결정 또는 오류 세부 정보가 포함된 XML 또는 JSON입니다. 아래 샘플을 참조하십시오. | 200 - 성공</br></br>400 - 잘못된 요청</br></br>401 - 권한 없음</br></br>405 - 메서드가 허용되지 않음  </br></br>412 - 전제 조건 실패</br></br>500 - 내부 서버 오류 |



| 입력 매개 변수 | 설명 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 등록 코드 | 인증 흐름 시작 시 사용자가 제공한 등록 코드 값입니다. |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| 리소스 목록 | 사용자가 액세스할 수 있고 MVPD 인증 끝점에서 인식되는 콘텐츠를 식별하는 쉼표로 구분된 resourceIds 목록을 포함하는 문자열입니다. |


### 샘플 응답 {#sample-response}

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4`
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
    <resource>
        <id>TestStream1</id>
        <authorized>true</authorized>
    </resource>
    <resource>
        <id>TestStream2</id>
        <authorized>false</authorized>  
        <error>
            <status>403</status>
            <code>authorization_denied_by_mvpd</code>
            <message>User not authorized</message>
            <details>Your subscription package does not include the "TestStream3" channel.</details>
            <helpUrl>https://tve.helpdocsonline.com/errors/preauthorization_denied</helpUrl>
            <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
            <action>none</action>
        </error>
    <resource>
</resources>
```

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://tve.helpdocsonline.com/errors/preauthorization_denied",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
 

### [REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
