---
description: FairPlay 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
title: FairPlay 라이선스 토큰 요청/응답
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# FairPlay 라이선스 토큰 요청 및 응답 {#fairplay-license-token-request-response}

FairPlay 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다. 이 요청은 FairPlay 라이선스로 상환할 수 있는 토큰을 반환합니다.

**방법: GET, POST** (두 메서드의 매개 변수가 포함된 www-url로 인코딩된 본문 사용)

**URL:**

* **프로덕션:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **테스트:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **샘플 요청:**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **샘플 응답:**

  ```
  https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
  ```

**요청 쿼리 매개 변수**

**표 3: 토큰 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| customerAuthenticator 쿼리 매개 변수로서의 고객 인증자 customerAuthenticator FairPlay | 프로덕션 및 테스트 환경에 대해 각각 하나씩 제공되는 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 찾을 수 있습니다. | 예 |
| errorFormat | html 또는 json입니다. html(기본값)인 경우 오류의 HTML 표현이 응답의 엔티티 본문에서 제공됩니다. json이 지정된 경우 JSON 형식의 구조화된 응답이 반환됩니다. 다음을 참조하십시오 [JSON 오류](https://www.expressplay.com/developer/restapi/#json-errors) 을 참조하십시오. 응답의 MIME 유형은 성공 시 text/uri-list, HTML 오류 형식인 text/html 또는 JSON 오류 형식인 application/json입니다. | 아니요 |

**표 4: 라이선스 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `generalFlags` | 라이선스 플래그를 나타내는 4바이트의 16진수 문자열입니다. &#39;0000&#39;만 사용할 수 있습니다. | 아니요 |
| `kek` | 키 암호화 키(KEK). 키는 키 래핑 알고리즘(AES Key Wrap, RFC3394)을 사용하여 KEK로 암호화되어 저장됩니다. If `kek` 다음 중 한 방법으로 제공됩니다. `kid` 또는 `ek` 매개 변수를 제공해야 합니다. *하지만 둘 다*. | 아니요 |
| `kid` | 콘텐츠 암호화 키 또는 문자열의 16바이트 16진수 문자열 표현 `'^somestring'`. 뒤에 오는 문자열의 길이 `'^'` 64자를 초과할 수 없습니다. | 아니요 |
| `ek` | 암호화된 콘텐츠 키의 16진수 문자열 표현입니다. | 아니요 |
| `contentKey` | 콘텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예, 그렇지 않은 경우 `kek` 및 `ek` 또는 `kid` 제공됩니다. |
| `iv` | 콘텐츠 암호화 IV의 16바이트 16진수 문자열 표현 | 예 |
| `rentalDuration` | 대여 기간(초)(기본값 - 0) | 아니요 |
| `fpExtension` | 간단한 포장으로 된 것 `extensionType` 및 `extensionPayload`쉼표로 구분된 문자열입니다. 예: [...] `&fpExtension=wudo,AAAAAA==&`[...] | 아니요, 모든 숫자를 사용할 수 있습니다. |

**표 5: 토큰 제한 쿼리 매개 변수**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>쿼리 매개 변수</b> </th> 
   <th class="entry"> <b>설명</b> </th> 
   <th class="entry"> <b>필수?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> 이 토큰의 만료 시간. 이 값은 의 문자열이어야 합니다. <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 'Z' 영역 지정자의 날짜/시간 형식("Zulu time") 또는 앞에 '+' 기호가 있는 정수. RFC 3339 날짜/시간의 예는 다음과 같습니다. <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>값이 의 문자열인 경우 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 날짜/시간 형식인 경우 토큰의 절대 만료 날짜/시간을 나타냅니다. 값이 앞에 '+' 기호가 있는 정수인 경우 토큰이 유효하다는 발급 후 상대적 초 수로 해석됩니다. </p> 예를 들어, <span class="codeph"> +60 </span> 1분을 지정합니다. 최대 및 기본(지정되지 않은 경우) 토큰 수명은 30일입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 6: 상관 관계 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `cookie` | 토큰에 전달되고 토큰 상환 서버에 의해 기록되는 최대 32자의 임의 문자열. 이를 사용하여 상환 서버의 로그 항목과 서비스 공급자 서버의 로그 항목을 상호 연관시킬 수 있습니다. | 아니요 |

**응답**

**표 7: HTTP 응답**

| **HTTP 상태 코드** | **설명** | **Content-Type** | **엔티티 본문이 다음을 포함** |
|---|---|---|---|
| `200 OK` | 오류 없음. | `text/uri-list` | 라이선스 획득 URL + 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` 또는 `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` 또는 `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` 또는 `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` 또는 `application/json` | 오류 설명 |

**표 8: 이벤트 오류 코드**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>코드</b> </th> 
   <th class="entry"> <b>설명</b> </th> 
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
   <td> 잘못된 인증 토큰: &lt;details&gt; <p>참고: 이 문제는 인증자가 잘못되었거나 의 테스트 API에 액세스할 때 발생할 수 있습니다. <span class="filepath"> *.test.expressplay.com </span> 프로덕션 인증자를 사용하거나 그 반대로 사용합니다. </p> <p importance="high">참고: SDK 및 ATT(고급 테스트 도구)는 <span class="filepath"> *.test.expressplay.com </span>, 반면에 프로덕션 디바이스는 <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 사용 가능한 토큰이 충분하지 않음 </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> 권한 유형 누락 </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> 잘못된 권한 유형 </td> 
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
   <td> 미아 </td> 
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
   <td> <span class="codeph"> 아이 </span> ^ 뒤에 64자가 있어야 합니다. </td> 
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
   <td> -6001 </td> 
   <td> 잘못됨 <span class="codeph"> FPExtension </span> 지정된 매개 변수 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> 잘못된 FP 토큰 유형 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 잘못됨 <span class="codeph"> iv </span> 매개 변수가 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> FP에 대한 CKC 생성 실패 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 잘못된 키 데이터가 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> 서비스가 FairPlay 지원에 대해 승인되지 않음 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 잘못된 임대 기간이 지정됨 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> 장치 ID 바인딩은 FairPlay에 대해 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> FairPlay 옵션이 비활성화됨 </td> 
  </tr> 
 </tbody> 
</table>
