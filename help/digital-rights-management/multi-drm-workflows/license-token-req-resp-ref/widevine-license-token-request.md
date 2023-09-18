---
description: Widevine 라이센스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
title: Widevine 라이선스 토큰 요청/응답
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# Widevine 라이선스 토큰 요청/응답 {#widevine-license-token-request-response}

Widevine 라이센스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.

이 HTTP 요청은 Widevine 라이선스에 대해 상환할 수 있는 토큰을 반환합니다.

**방법: GET, POST** (두 메서드의 매개 변수가 포함된 www-url로 인코딩된 본문 사용)

**URL:**

* **프로덕션:** `https://wv-gen.{prod_domain}/hms/wv/token`

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

**표 13: 토큰 쿼리 매개 변수**

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
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>프로덕션 및 테스트 환경에 대해 각각 하나씩 제공되는 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 찾을 수 있습니다. </p> </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> 다음 중 하나 <span class="codeph"> html </span> 또는 <span class="codeph"> json </span>. <p>If <span class="codeph"> html </span> (기본값) 모든 오류의 HTML 표현은 응답의 엔티티 본문에서 제공됩니다. If <span class="codeph"> json </span> 을 지정하면 JSON 형식의 구조화된 응답이 반환됩니다. 다음을 참조하십시오 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON 오류 </a> 을 참조하십시오. </p> <p>응답의 mime 유형은 다음 중 하나입니다. <span class="codeph"> text/uri-list </span> 성공 시, <span class="codeph"> text/html </span> 대상 <span class="codeph"> html </span> 오류 형식 또는 <span class="codeph"> application/json </span> 대상 <span class="codeph"> json </span> 오류 형식입니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 14: 라이선스 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| `generalFlags` | 라이선스 플래그를 나타내는 4바이트의 16진수 문자열입니다. &#39;0000&#39;만 허용되는 값입니다. | 아니요 |
| `kek` | 키 암호화 키(KEK). 키는 키 래핑 알고리즘(AES Key Wrap, RFC3394)을 사용하여 KEK로 암호화되어 저장됩니다. | 아니요 |
| `kid` | 콘텐츠 암호화 키 또는 문자열의 16바이트 16진수 문자열 표현 `^somestring'`. 뒤에 오는 문자열의 길이 `^` 64자를 초과할 수 없습니다. 예를 보려면 아래 참고 사항을 확인하십시오. | 예 |
| `ek` | 암호화된 콘텐츠 키의 16진수 문자열 표현입니다. | 아니요 |
| `contentKey` | 콘텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예, 그렇지 않으면 `kek` 및 `ek` 또는 `kid` 제공됨 |
| `contentId` | 컨텐츠 Id | 아니요 |
| `securityLevel` | 허용되는 값은 1-5입니다. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 예 |
| `hdcpOutputControl` | 허용되는 값은 0, 1, 2입니다. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 예 |
| `licenseDuration` * | 라이선스 기간(초)입니다. 제공하지 않을 경우 지속 시간에 제한이 없음을 나타냅니다. 자세한 내용은 아래 참고 사항을 확인하십시오. | 아니요 |
| `wvExtension` | extensionType 및 extensionPayload를 쉼표로 구분된 문자열로 줄바꿈하는 짧은 양식입니다. 아래 형식을 참조하십시오. 예: `…&wvExtension=wudo,AAAAAA==&…` | 아니요, 모든 숫자를 사용할 수 있습니다. |

정보 `licenseDuration`: <ol><li> 재생이 중지됨 `licenseDuration` 재생 시작 후(초). </li><li> 재생이 시간 제한 없이 중단/재개될 수 있도록 하려면 을 생략합니다 `licenseDuration` (기본값은 무한대입니다.) 또는 최종 사용자가 스트림을 즐길 수 있는 시간을 지정합니다. </li></ol>

**표 15: 토큰 제한 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| `expirationTime` | 이 토큰의 만료 시간. 이 값은 다음 문자열에 있어야 합니다. [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) &#39;Z&#39; 영역 지정자의 날짜/시간 형식(&quot;줄루 시간&quot;) 또는 앞에 + 기호가 오는 정수입니다. RFC 3339 날짜/시간의 예는 2006-04-14T12입니다.:01:10Z <br> 값이 의 문자열인 경우 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 날짜/시간 형식인 경우 토큰의 절대 만료 날짜/시간을 나타냅니다. 값이 앞에 + 기호가 있는 정수이면 토큰이 유효하다는 것을 발급한 시점부터 상대적 시간(초)으로 해석됩니다. 예를 들어, `+60` 1분을 지정합니다. <br> 최대 및 기본(지정되지 않은 경우) 토큰 수명은 30일입니다. | 아니요 |

**표 16: 상관 관계 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `cookie` | 토큰에 전달되고 토큰 상환 서버에 의해 기록된 최대 32자의 임의 문자열. 서비스 공급자 서버의 로그 항목과 상환 서버의 로그 항목을 상호 연결하는 데 사용할 수 있습니다. | 아니요 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**표 17: HTTP 응답**

| **HTTP 상태 코드** | **설명** | **Content-Type** | **엔티티 본문이 다음을 포함** |
|---|---|---|---|
| `200 OK` | 오류 없음. | `text/uri-list` | 라이선스 획득 URL + 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` 또는 `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` 또는 `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` 또는 `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` 또는 `application/json` | 오류 설명 |

**표 18: 이벤트 오류 코드**

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
   <td> 잘못된 토큰 만료 시간: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 잘못된 IP 주소 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 잘못된 콘텐츠 암호화 키: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 잘못된 출력 제어 플래그가 지정되었습니다. &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 인증 토큰을 제공해야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 잘못된 인증 토큰: &lt;details&gt; <p>참고: 인증자가 잘못되었거나 프로덕션 인증자를 사용하여 *.test.expressplay.com에서 테스트 API에 액세스하거나 그 반대의 경우 이 문제가 발생할 수 있습니다. </p> <p importance="high">참고: SDK 및 ATT(고급 테스트 도구)는 <span class="filepath"> *.test.expressplay.com </span>, 반면에 프로덕션 디바이스는 <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 사용 가능한 토큰이 충분하지 않음 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 임대 기간 종료 시간 누락 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 대여 재생 기간 누락 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 잘못된 대여 재생 기간 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 콘텐츠 암호화 키는 32자리 16진수여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay 관리자 오류: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 서비스 계정 비활성화됨 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> 잘못된 쿠키 </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> 출력 제어가 잘못되었습니다. 값이 지정된 범위를 벗어났습니다. </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> 해당 값이 지정되지 않음 </td> 
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
   <td> <span class="codeph"> OutputControlFlag </span> 은(는) 인코딩해야 합니다 4바이트 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 잘못된 오류 형식이 지정되었습니다. &lt;format&gt; </td> 
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
   <td> 누락 <span class="filepath"> 아이 </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 키 저장소 서비스에서 콘텐츠 키를 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> 아이 </span> 은(는) 32개의 16진수 문자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 아이 </span> 은(는) '^' 뒤에 64자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 잘못됨 <span class="codeph"> 아이 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 잘못된 암호화 키 또는 <span class="codeph"> 케크 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 잘못된 일반 플래그 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 잘못된 키 데이터가 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 잘못된 임대 기간이 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> 장치 ID 바인딩은 Widevine에서 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 보안 수준 값 누락 </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 잘못된 보안 수준 값 </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> HDCP 출력 제어 값 누락 </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> 잘못된 라이선스 기간이 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Widevine 라이센스 생성 실패 </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 잘못됨 <span class="codeph"> WVExtension </span> 지정된 매개 변수 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Widevine 옵션 비활성화됨 </td> 
  </tr> 
 </tbody> 
</table>
