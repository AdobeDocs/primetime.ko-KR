---
title: /authenticate 요청에서 '&'reg_code를 사용하지 마십시오.
description: /authenticate 요청에서 '&'reg_code를 사용하지 마십시오.
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# /authenticate 요청에서 &#39;&amp;&#39;reg_code를 사용하지 마십시오. {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>



## 문제

IE 9 브라우저는 &#39;\®&#39;을(를) 특수 명령으로 해석하여 ®. 

## 설명

만약 `/authenticate` 요청은 다음과 같이 구성됩니다.

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...아래와 같이 IE 브라우저가 해석하며 이 형식으로 Adobe으로 전송됩니다.

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

요청자\_id는 &#39;&amp;&#39;가 없으므로 univision®\_code=EKAFMFI로 해석되며 Adobe은 `regCode` 토큰과 연결할 매개 변수입니다.  AuthN 토큰이 전혀 생성되지 않을 가능성이 있습니다. 이 경우 `/checkauthn` 호출에서 토큰을 찾지 못합니다.



## 솔루션

다음 옵션 중 하나를 사용하면 이 문제를 해결할 수 있습니다.

1. 를 사용하지 마십시오 `&reg_code` 다른 쿼리 문자열 매개 변수 사이의 매개 변수입니다.  대신 요청 URL의 첫 번째 쿼리 문자열 매개 변수로 이동하여 다음과 같이 요청 URL을 만듭니다.\
    

       &lt;fqdn>authenticate?reg_code = EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   이렇게 하면 `&reg` 매개 변수가 잘못 해석되지 않습니다.

1. 정규화 `&reg_code` 사용 `&amp;reg_code`.

1. AuthN 토큰 만들기에 실패한 경우 Adobe에서 인증 호출에 대한 응답으로 오류 코드를 두 번째 화면으로 다시 보내는 새 기능을 도입할 수 있습니다.

