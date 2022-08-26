---
title: 인증 시작
description: 인증 시작
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# 인증 시작 {#initiate-authentication}

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

MVPD 선택 이벤트를 알리고 인증 프로세스를 시작합니다. MVPD에서 성공적인 응답을 받을 때 조정되는 Primetime 인증 데이터베이스에 레코드를 만듭니다. 



| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | AuthN 모듈 | 1. requestor_id(필수)</br>2.  mso_id(필수)</br>3.  reg_code(필수)</br>4.  domain_name(필수)</br>5.  noflash=true -  </br>    (필수, 남은 매개변수)</br>6.  no_iframe=true(필수, 잔여 매개 변수)</br>7.  추가 매개 변수(선택 사항)</br>8.  redirect_url(필수) | GET | 로그인 웹 앱이 MVPD 로그인 페이지로 리디렉션됩니다. | 전체 리디렉션 구현에 대한 302 |

{style=&quot;table-layout:auto&quot;}


| 입력 매개 변수 | 설명 |
| --- | --- |
| requestor_id | 이 작업이 유효한 프로그래머 요청자입니다. |
| mso_id | 이 작업이 유효한 MVPD ID입니다. |
| reg_code | 레지 서비스에서 생성한 등록 코드입니다. |
| domain_name | 원래 도메인. |
| redirect_url | 인증 완료 후 로그인 웹 앱 리디렉션 URL입니다. |

{style=&quot;table-layout:auto&quot;}

</br>

>[!IMPORTANT]
> 
>**중요 사항: 필수 매개 변수 -** 클라이언트측 구현에 관계없이 위의 모든 매개 변수는 필수입니다.
>
>
>예:    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**중요 사항: 선택적 매개 변수**
>
>호출에는 다음과 같은 다른 기능을 활성화하는 선택적 매개 변수가 포함될 수도 있습니다.
>
> * generic\_data - [프로모션 TempPass](https://tve.helpdocsonline.com/promotional-temp-pass)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **참고** {#notes}

* 의 값 `domain_name` 매개 변수는 Primetime 인증과 함께 등록된 도메인 이름 중 하나로 설정해야 합니다. 자세한 내용은 [등록 및 초기화](http://tve.helpdocsonline.com/new-programmer-overview$reg_and_init).

* [/authenticate 요청에서 &#39;&amp;&#39;reg\_code를 사용하지 마십시오(기술 참고)](https://tve.helpdocsonline.com/clientless:-avoid-using-&#39;&amp;&#39;reg_code-in-/authenticate-request)

* 다음 `redirect_url` 매개 변수는 순서대로 마지막 매개 변수여야 합니다.

* 의 값 `redirect_url` 매개 변수는 URL로 인코딩되어야 합니다.

[REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
