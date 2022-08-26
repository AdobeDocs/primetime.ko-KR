---
title: Adobe 토큰에 대해 플랫폼 SSO 토큰 교환
description: Adobe 토큰에 대해 플랫폼 SSO 토큰 교환
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 2%

---


# Adobe 토큰에 대해 플랫폼 SSO 토큰 교환 {#exchange-a-platform-sso-token-for-an-adobe-token}

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

Adobe 토큰에 대해 Platform SSO 프로필을 &quot;교환&quot;할 수 있도록 허용합니다.

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(필수)</br>    </br>2.  deviceId(필수)</br>    </br>3.  mvpd(필수)</br>    </br>4.  deviceType(필수)</br>    </br>5.  SAMLResponse(필수)</br>    </br>6.  deviceUser(사용 중지)</br>    </br>7.  appId(더 이상 사용되지 않음) | POST | 성공적인 응답은 토큰이 성공적으로 만들어졌고 인증 흐름에 사용할 준비가 되었음을 나타내는 204 컨텐츠 없음이 됩니다. | 204 - 컨텐츠 없음   </br>400 - 잘못된 요청 |


| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| mvpd | 이 작업이 유효한 MVPD ID입니다. |
| deviceType | 프로필 요청을 받으려는 Apple 플랫폼입니다.  다음 중 하나 **iOS** 또는 **tvOS**. |
| SAMLResponse | 플랫폼 SSO에서 반환된 실제 프로필입니다. |
| _deviceUser_ | 장치 사용자 식별자입니다. |
| _appId_ | 애플리케이션 ID/이름입니다. |



### [REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
