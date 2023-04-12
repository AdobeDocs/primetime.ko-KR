---
title: 등록 레코드 삭제
description: 등록 리소스 삭제
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 등록 레코드 삭제 {#delete-registration-record}

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


## 설명 {#delete-record}

reg 코드 레코드를 삭제하고 재사용할 reg 코드를 해제합니다. 

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/register/v1/{requestorId}/regcode/{registrationCode}</br></br>예:</br></br>&lt;reggie_fqdn>/register/v1/regcode/ER45RTY | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자 ID  </br>    (경로 구성 요소)</br>2.  등록 코드  </br>    (경로 구성 요소) | DELETE | 없음 | 204 |

{style="table-layout:auto"}

</br>

| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| 등록 코드 | 스트리밍 장치(인증 플로우에 입력)에 표시될 등록 코드 값입니다. |

{style="table-layout:auto"}

</br>

### [REST API 참조로 돌아가기](/help/authentication/rest-api-reference.md)
