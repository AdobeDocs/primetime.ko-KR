---
description: 무선 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
title: 무선 라이선스 토큰 요청/응답
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---


# 무선 라이선스 토큰 요청 / 응답 {#widevine-license-token-request-response}

무선 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.

이 HTTP 요청은 무선 라이선스로 상환할 수 있는 토큰을 반환합니다.

**방법:GET, POST** (두 메서드의 매개 변수를 포함하는 www-url 인코딩 본문 포함)

**URL:**

* **제작:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **테스트:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **샘플 요청:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **샘플 응답:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**표 13:토큰 쿼리 매개 변수**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>쿼리 매개 변수</b> </th> 
   <th class="entry"> <b>설명</b> </th> 
   <th class="entry"> <b>필수?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator  </span> </td> 
   <td> <p>프로덕션 및 테스트 환경에 적합한 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 확인할 수 있습니다. </p> </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat  </span> </td> 
   <td> <span class="codeph"> html </span> 또는 <span class="codeph"> json </span> 중 하나를 선택합니다. <p><span class="codeph"> html </span>(기본값)인 경우 응답의 엔티티 본문에 모든 오류에 대한 HTML 표현이 제공됩니다. <span class="codeph"> json </span>이 지정된 경우 JSON 형식의 구조화된 응답이 반환됩니다. 자세한 내용은 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON 오류 </a>를 참조하십시오. </p> <p>응답의 MIME 유형은 성공한 경우 <span class="codeph"> text/uri-list </span>, <span class="codeph"> html </span> 오류 포맷의 경우 <span class="codeph"> text/html </span>, <span class="codeph"> json </span> 오류 포맷의 경우 <span class="codeph"> application/json </span> 입니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 14:라이센스 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| `generalFlags` | 라이센스 플래그를 나타내는 4바이트 16진수 문자열입니다. &#39;0000&#39;은(는) 유일하게 허용되는 값입니다. | 아니요 |
| `kek` | 키 암호화 키(KEK). 키는 키 흐름 알고리즘을 사용하여 KEK를 사용하여 암호화됩니다(AES 키 랩, RFC3394). | 아니요 |
| `kid` | 컨텐츠 암호화 키 또는 문자열 `^somestring'`의 16바이트 16진수 문자열 표현입니다. 문자열 뒤에 `^`이 오는 길이는 64자보다 길 수 없습니다. 예를 보려면 아래 메모를 확인하십시오. | 예 |
| `ek` | 암호화된 콘텐츠 키의 16진 문자열 표현입니다. | 아니요 |
| `contentKey` | 컨텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예, `kek` 및 `ek` 또는 `kid`가 제공되지 않는 한 |
| `contentId` | 콘텐츠 ID | 아니요 |
| `securityLevel` | 허용되는 값은 1-5입니다. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 예 |
| `hdcpOutputControl` | 허용되는 값은 0, 1, 2입니다. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 예 |
| `licenseDuration` * | 라이선스 기간(초) 제공되지 않으면 기간에 제한이 없음을 나타냅니다. 자세한 내용은 아래 노트를 확인하십시오. | 아니요 |
| `wvExtension` | 짧은 양식 래핑 확장자Type 및 extensionPayload를 쉼표로 구분된 문자열로 나타냅니다. 아래 형식을 참조하십시오. 예:`…&wvExtension=wudo,AAAAAA==&…` | 아니오 아무 번호나 사용할 수 있습니다 |

`licenseDuration` 정보: <ol><li> 재생이 시작된 후 `licenseDuration`초 후에 재생이 중지됩니다. </li><li> 제한 없는 시간 동안 재생을 중지/다시 시작하려면 `licenseDuration`을(를) 생략하십시오(기본적으로 무한으로 설정됨). 그렇지 않으면 최종 사용자가 스트림을 즐길 수 있는 시간을 지정합니다. </li></ol>

**표 15:토큰 제한 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| `expirationTime` | 이 토큰의 만료 시간입니다. 이 값은 &#39;Z&#39; 영역 지정자(&quot;Zulu time&quot;)에 있는 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 날짜/시간 형식의 문자열이나 + 기호 앞에 오는 정수여야 합니다. RFC 3339 날짜/시간의 예는 2006-04-14T12:01:10Z입니다. <br> 값이 RFC 3339  [](https://www.ietf.org/rfc/rfc3339.txt) 날짜/시간 형식의 문자열이면 토큰에 대한 절대 만료 날짜/시간을 나타냅니다. 값이 + 기호 앞에 오는 정수인 경우 발행부터 해당 토큰이 유효하다는 상대 시간(초)으로 해석됩니다. 예를 들어 `+60`은 1분을 지정합니다. <br> 최대 및 기본(지정되지 않은 경우) 토큰 수명은 30일입니다. | 아니요 |

**표 16:상관 관계 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `cookie` | 토큰에 들어 있고 토큰 상환 서버에서 로깅하는 최대 32자의 임의의 문자열입니다. 등록 서버와 서비스 공급자의 서버에 있는 로그 항목의 상관 관계를 지정할 수 있습니다. | 아니요 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**표 17:HTTP 응답**

| **HTTP 상태 코드** | **설명** | **컨텐츠 유형** | **엔티티 본문에 포함** |
|---|---|---|---|
| `200 OK` | 오류가 없습니다. | `text/uri-list` | 라이센스 획득 URL + 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` or  `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` or  `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` or  `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` or  `application/json` | 오류 설명 |

**표 18:이벤트 오류 코드**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> 코드 </th> 
   <th class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 잘못된 토큰 만료 시간:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 잘못된 IP 주소 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 잘못된 콘텐츠 암호화 키:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 잘못된 출력 제어 플래그 지정:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017년 </td> 
   <td> 인증 토큰을 제공해야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2018년 </td> 
   <td> 인증 토큰이 잘못되었습니다.&lt;details&gt; <p>참고: 인증자가 잘못되거나 *.test.express.com에서 프로덕션 인증자를 사용하여 테스트 API에 액세스하거나 그 반대로 액세스할 때 발생할 수 있습니다. </p> <p importance="high">참고: 테스트 SDK 및 고급 테스트 도구(ATT)는 <span class="filepath"> *.test.express.com </span>에서만 작동하지만 프로덕션 장치는 <span class="filepath"> *.service.express.com </span>을 사용해야 합니다. </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019년 </td> 
   <td> 사용할 수 있는 토큰 부족 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 임대 기간 종료 시간 누락 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 대여 재생 기간이 누락됨 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 대여 재생 기간이 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 컨텐츠 암호화 키는 32개의 16진수 숫자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay 관리자 오류:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 서비스 계정 비활성화 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> 잘못된 쿠키 </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> 출력 컨트롤이 잘못되었습니다. 값이 지정된 범위를 벗어났습니다. </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> 해당 값이 지정되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> 확장 유형은 4자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 확장 페이로드는 Base64로 인코딩되어야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag는 4바이트를 인코딩해야  </span> 합니다. </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 잘못된 오류 형식을 지정했습니다.&lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> 장치를 인증할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> 잘못된 토큰 </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> <span class="filepath"> 하위 </span> 없음 </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 키 저장소 서비스에서 콘텐츠 키를 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> kid는 32자의 16진수 문자여야  </span> 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 어린이는 '^' 뒤에 64자여야  </span> 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 잘못된 <span class="codeph"> 하위 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 잘못된 암호화된 키 또는 <span class="codeph"> 키 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 잘못된 일반 플래그 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 잘못된 키 데이터가 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 잘못된 임대 기간이 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> 장치 ID 바인딩은 Widevine에 대해 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 보안 수준 값이 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 잘못된 보안 수준 값 </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> HDCP 출력 제어 값이 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> 잘못된 라이센스 기간이 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> 무선 라이선스를 생성하지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 잘못된 <span class="codeph"> WVExtension </span> 매개 변수가 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> 무선 옵션을 사용할 수 없음 </td> 
  </tr> 
 </tbody> 
</table>