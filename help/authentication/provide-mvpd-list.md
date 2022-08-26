---
title: MVPD 목록 제공
description: MVPD 목록 제공
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# MVPD 목록 제공 {#provide-mvpd-list}

## REST API 엔드포인트 {#clientless-endpoints}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## 설명 {#description}

요청자에 대해 구성된 MVPD 목록을 반환합니다.

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>예:</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Primetime 인증 | 1. 요청자</br>    (경로 구성 요소)</br>_2.  deviceType(지원 중단됨)_ | GET | MVPD 목록이 포함된 XML 또는 JSON입니다. | 200년 |

{style=&quot;table-layout:auto&quot;}


| 입력 매개 변수 | 설명 |
| --------------- | ------------------------------------------------------------- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| *deviceType* | 장치 유형. |

{style=&quot;table-layout:auto&quot;}

### 샘플 응답 {#sample-response}

/config 서블릿에 대한 기존 MVPD XML 응답과 동일

참고: Platform SSO를 사용하도록 구성된 모든 MVPD에는 해당 노드(JSON/XML) 내에 다음과 같은 추가 속성이 있습니다.

* **enablePlatformServices(부울):** 이 MVPD가 플랫폼 SSO를 통해 통합되었는지 여부를 나타내는 플래그
* **boardingStatus (string):** MVPD가 플랫폼 SSO(SUPPORTED)를 완전히 지원하는지 또는 MVPD가 플랫폼 선택기(PICKER)에만 표시되는지를 나타내는 플래그입니다
* **displayInPlatformPicker(부울):** 이 MVPD가 플랫폼 선택기에 표시되어야 함
* **platformMappingId(문자열):** 플랫폼에 의해 알려진 이 MVPD의 식별자입니다.
* **requiredMetadataFields(문자열 배열):** 성공적인 로그인 시 사용자 메타데이터 필드를 사용할 수 있어야 합니다.


[Clientless API 참조로 돌아가기](http://tve.helpdocsonline.com/clientless-api-reference)
