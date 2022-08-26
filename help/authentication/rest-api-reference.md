---
title: REST API 참조
description: Rest api 참조
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# REST API 참조 {#rest-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 응답 형식 {#response-formats}


>[!NOTE]
>
> 이러한 서비스에 제공된 API는 XML 또는 JSON(응답을 반환하는 API의 경우)으로 응답을 반환할 수 있습니다. 요청에서 응답 형식을 지정하는 방법에는 3가지가 있습니다.
>* HTTP Accept 헤더를 &quot;application/xml&quot;로 설정합니다.</code>&quot; 또는 &quot;application/json&quot;</code>&quot;
>* 요청 페이로드에서 매개 변수 &quot;format=xml을 지정합니다</code>&quot; 또는 &quot;format=json&quot;</code>&quot;</li>
>* 확장명이 .xml인 웹 서비스 끝점을 호출합니다</code> 또는 .json</code>. 예: &quot;/regcode.xml</code>또는 &quot;/regcode.json</code>&quot;
>
>위의 메서드 중 하나를 지정할 수 있습니다. 형식이 충돌하는 여러 메서드를 지정하면 오류 또는 원치 않는 출력이 발생할 수 있습니다.

## REST API 엔드포인트 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 웹 서비스 요약 {#web_srvs_summary}

아래 표에는 clientless 접근 방식으로 사용 가능한 웹 서비스가 나와 있습니다. 자세한 내용(샘플 요청 및 응답, 입력 매개 변수, HTTP 메서드 등)을 보려면 웹 서비스 끝점을 클릭합니다.


| Sr | 웹 서비스 끝점 | 설명 | [디그  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | 호스팅 위치 | 호출자 |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/regee/v1/  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | 임의로 생성된 등록 코드 및 로그인 페이지 URI 반환 | 2개 | Adobe  </br>등록 코드 서비스 | 스마트 장치 |
| 2. | [&lt;reggie_fqdn>/regee/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | 등록 코드 UUID, 등록 코드 및 해시된 장치 ID가 포함된 등록 코드 레코드를 반환합니다 | 8 | Adobe  </br>등록 코드 서비스 | Primetime 인증 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | 요청자에 대해 구성된 MVPD 목록을 반환합니다. | 5개 | Adobe  </br>Primetime  </br>인증  </br>서비스 | 로그인  </br>웹  </br>앱 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](http://tve.helpdocsonline.com/initiate-authentication) | MVPD 선택 이벤트를 알려 AuthN 프로세스를 시작합니다. MVPD에서 성공적인 응답을 받을 때 조정되는 인증 데이터베이스에 대한 레코드를 만듭니다(13단계) | 7 | Adobe  </br>Primetime  </br>인증  </br>서비스 | 로그인  </br>웹  </br>앱 |
| 5. | SAML 검증 소비자 | Primetime 인증과 MVPD 간의 기존 SAML 워크플로우 | 13 | Primetime  </br>인증  </br>서비스 | Primetime 인증 |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | 로그인 웹 앱은 시도한 로그인 흐름이 성공했는지 확인할 수 있습니다 |  | Primetime  </br>인증   </br>서비스 | 로그인   </br>웹   </br>앱 |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | AuthN 토큰 관련 메타데이터 가져오기 | 15 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 8. | [&lt;reggie_fqdn>/regee/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | reg 코드 레코드를 삭제하고 재사용할 reg 코드를 해제합니다 | 16 | Adobe  </br>등록 코드 서비스 | Primetime 인증 |
| 9. | [&lt;sp_fqdn>/api/v1/authorization](http://tve.helpdocsonline.com/initiate-authorization) | 인증 응답을 가져옵니다. | 17 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | 장치에 만료되지 않은 AuthN 토큰이 있는지 여부를 나타냅니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | AuthN 토큰이 있는 경우 반환됩니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | AuthZ 토큰이 있는 경우 반환됩니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | /api/v1/mediattoken과 동일한 경우 짧은 미디어 토큰 반환 |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 14. | [&lt;sp_fqdn>/api/v1/mediattoken](http://tve.helpdocsonline.com/obtain-short-media-token) | 짧은 미디어 토큰 가져오기 |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorization](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | 사전 권한 리소스 목록을 검색합니다 |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorization/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | 사전 권한 리소스 목록을 검색합니다 |  | Primetime  </br>인증  </br>서비스 | 로그인 웹 앱 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | 저장소에서 AuthN 및 AuthZ 토큰 제거 |  | Primetime  </br>인증   </br>서비스 | 스마트 장치 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | 인증 흐름이 완료된 후 사용자 메타데이터를 가져옵니다. | 해당 없음 | 해당 없음 | 스마트 장치 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | 임시 패스 또는 프로모션 임시 패스에 대한 인증 토큰 만들기 | 해당 없음 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |

{style=&quot;table-layout:auto&quot;}

## REST API 보안 {#security}

모든 Primetime 인증 clientless API는 보안 통신을 위해 HTTPS 프로토콜을 사용하여 호출해야 합니다. 또한 호출된 대부분의 API는 [동적 클라이언트 등록](http://tve.helpdocsonline.com/dynamic-client-registration).


## 관련 정보 {#related}

* [REST API 개요](http://tve.helpdocsonline.com/reset-api-overview)
* [서버 간 Cookbook](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [클라이언트-서버 Cookbook](http://tve.helpdocsonline.com/client-to-server)
* [/authenticate 요청에서 &#39;&amp;&#39;reg\_code를 사용하지 마십시오(기술 참고)](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
