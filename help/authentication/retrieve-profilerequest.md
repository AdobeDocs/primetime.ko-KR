---
title: 플랫폼 SSO 프로필 요청 검색
description: 플랫폼 SSO 프로필 요청 검색
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 플랫폼 SSO 프로필 요청 검색 {#retrieve-platform-sso-profile-request}

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

이 리소스는 요청자 ID 및 MVPD 튜플에 대한 프로필 요청을 생성합니다.


| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(경로 매개 변수)</br>2. mvpd(경로 매개 변수)</br>3. deviceType(필수) | GET | 실제 페이로드가 클라이언트 응용 프로그램에 대해 불투명하므로 응답 Content-Type은 application/octet-stream입니다.</br></br>응용 프로그램에서 플랫폼으로 응답을 전달해야 합니다</br></br>프로필 SSO를 얻기 위한 SSO 엔진입니다. | 200 - 성공   </br>400 - 잘못된 요청 |


| 입력 매개 변수 | 설명 |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| mvpd | 이 작업이 유효한 MVPD ID입니다. |
| deviceType | 프로필 요청을 받으려는 Apple 플랫폼입니다.  다음 중 하나 **iOS** 또는 **tvOS**. |


