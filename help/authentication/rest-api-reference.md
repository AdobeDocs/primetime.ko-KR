---
title: REST API 참조
description: Rest api 참조
exl-id: 67e4639e-db0b-4400-bb81-e214263e8395
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# REST API 참조 {#rest-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## 응답 형식 {#response-formats}


>[!NOTE]
>
> 이러한 서비스에 제공된 API는 XML 또는 JSON(응답을 반환하는 API의 경우)으로 응답을 반환할 수 있습니다. 요청에 응답 형식을 지정하는 방법에는 세 가지가 있습니다.
>
>* HTTP Accept 헤더 를 다음으로 설정 `application/xml` 또는 `application/json`.
>* 요청 페이로드에서 매개 변수를 지정합니다. `format=xml` 또는 `format=json`.
>* 확장을 사용하여 웹 서비스 끝점 호출 `.xml` 또는 `.json`. 예를 들어, `/regcode.xml` 또는 `/regcode.json`
>
>위의 방법 중 하나를 지정할 수 있습니다. 형식이 충돌하는 여러 메서드를 지정하면 오류가 발생하거나 원하지 않는 출력이 발생할 수 있습니다.

## REST API 끝점 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 웹 서비스 요약 {#web_srvs_summary}

아래 표에는 클라이언트 없는 접근 방식에 사용할 수 있는 웹 서비스가 나열되어 있습니다. 자세한 내용을 보려면 웹 서비스 끝점을 클릭합니다(샘플 요청 및 응답, 입력 매개 변수, HTTP 메서드 등).


| Sr | 웹 서비스 끝점 | 설명 | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | 호스팅 위치 | 호출자 |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | 임의로 생성된 등록 코드 및 로그인 페이지 URI를 반환합니다. | 2 | Adobe  </br>코드 서비스 등록 | 스마트 장치 |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | 등록 코드 UUID, 등록 코드 및 해시된 장치 ID가 포함된 등록 코드 레코드를 반환합니다. | 8 | Adobe  </br>코드 서비스 등록 | Primetime 인증 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | 요청자에 대해 구성된 MVPD 목록을 반환합니다. | 5 | Adobe  </br>Primetime  </br>인증  </br>서비스 | 로그인  </br>웹  </br>앱 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](/help/authentication/initiate-authentication.md) | MVPD 선택 이벤트를 알려 AuthN 프로세스를 시작합니다. MVPD로부터 성공적인 응답을 받으면 조정되는 인증 데이터베이스에 레코드를 만듭니다(13단계). | 7 | Adobe  </br>Primetime  </br>인증  </br>서비스 | 로그인  </br>웹  </br>앱 |
| 5. | SAML 어설션 소비자 | Primetime 인증과 MVPD 간의 기존 SAML 워크플로 | 13 | Primetime  </br>인증  </br>서비스 | Primetime 인증 |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | 로그인 웹 앱은 시도한 로그인 흐름이 성공했는지 확인할 수 있습니다 |  | Primetime  </br>인증   </br>서비스 | 로그인   </br>웹   </br>앱 |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | AuthN 토큰 관련 메타데이터 가져오기 | 15 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | 정규 코드 레코드를 삭제하고 재사용을 위해 정규 코드를 해제합니다. | 16 | Adobe  </br>코드 서비스 등록 | Primetime 인증 |
| 9. | [&lt;sp_fqdn>/api/v1/authorize](/help/authentication/initiate-authorization.md) | 인증 응답을 가져옵니다. | 17 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | 장치에 만료되지 않은 AuthN 토큰이 있는지 여부를 나타냅니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | 발견되면 AuthN 토큰을 반환합니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | 발견된 경우 AuthZ 토큰을 반환합니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | 발견된 경우 짧은 미디어 토큰 반환 - /api/v1/mediatoken과 동일 |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | 짧은 미디어 토큰 가져오기 |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 15. | [&lt;sp_fqdn>/api/v1/사전 승인](/help/authentication/retrieve-list-of-preauthorized-resources.md) | 사전 승인된 리소스 목록을 검색합니다. |  | Primetime  </br>인증  </br>서비스 | 스마트 장치 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorize/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | 사전 승인된 리소스 목록을 검색합니다. |  | Primetime  </br>인증  </br>서비스 | 로그인 웹 앱 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](/help/authentication/initiate-logout.md) | 저장소에서 AuthN 및 AuthZ 토큰 제거 |  | Primetime  </br>인증   </br>서비스 | 스마트 장치 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | 인증 흐름이 완료된 후 사용자 메타데이터를 가져옵니다. | 해당 사항 없음 | 해당 사항 없음 | 스마트 장치 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | 임시 패스 또는 프로모션 임시 패스에 대한 인증 토큰 만들기 | 해당 사항 없음 | Primetime  </br>인증  </br>서비스 | 스마트 장치 |


## REST API 보안 {#security}

모든 Primetime 인증 클라이언트 없는 API는 보안 통신을 위해 HTTPS 프로토콜을 사용하여 호출해야 합니다. 또한 호출된 대부분의 API는에서 제공하는 액세스 토큰을 포함해야 합니다. [동적 클라이언트 등록](/help/authentication/dynamic-client-registration.md).
