---
description: FairPlay 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
seo-description: FairPlay 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
seo-title: FairPlay 라이선스 토큰 요청/응답
title: FairPlay 라이선스 토큰 요청/응답
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---


# FairPlay 라이선스 토큰 요청 및 응답 {#fairplay-license-token-request-response}

FairPlay 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다. 이 요청은 FairPlay 라이선스로 상환될 수 있는 토큰을 반환합니다.

**메서드:GET, POST** (두 메서드에 대한 매개 변수를 포함하는 www-url 인코딩 본문 사용)

**URL:**

* **제작:** `https://fp-gen.{prod_domain}/hms/fp/token`

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

**표 3:토큰 쿼리 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수? |
|--- |--- |--- |
| customerAuthenticator 고객 인증자를 쿼리 매개 변수 고객인증자 FairPlay | 프로덕션 및 테스트 환경에 적합한 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 확인할 수 있습니다. | 예 |
| errorFormat | html 또는 json 중 하나. html(기본값)이 응답의 엔티티 본문에 오류의 HTML 표현을 제공하는 경우 json이 지정된 경우 JSON 형식의 구조화된 응답이 반환됩니다. 자세한 내용은 [JSON 오류를](https://www.expressplay.com/developer/restapi/#json-errors) 참조하십시오. 응답의 MIME 유형은 success의 텍스트/uri-list, HTML 오류 포맷의 텍스트/html 또는 JSON 오류 포맷의 application/json입니다. | 아니요 |

**표 4:라이센스 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `generalFlags` | 라이센스 플래그를 나타내는 4바이트 16진수 문자열입니다. &#39;0000&#39;은 허용된 유일한 값입니다. | 아니요 |
| `kek` | 키 암호화 키(KEK). 키는 키 래핑 알고리즘(AES 키 랩, RFC3394)을 사용하여 KEK로 암호화됩니다. 이 `kek` 가 제공되면 매개 변수 `kid` 중 하나 또는 매개 변수 `ek` 중 하나를 제공해야 *하지만 둘 다*&#x200B;제공되어서는 안됩니다. | 아니요 |
| `kid` | 컨텐츠 암호화 키 또는 문자열을 16바이트 16진수 문자열 표현입니다 `'^somestring'`. 문자열 뒤에 오는 길이는 64자보다 길 `'^'` 수 없습니다. | 아니요 |
| `ek` | 암호화된 콘텐츠 키의 16진수 문자열 표현. | 아니요 |
| `contentKey` | 컨텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예, `kek` 및 `ek` 또는 를 제공하지 `kid` 않는 한. |
| `iv` | 컨텐츠 암호화 IV의 16바이트 16진수 문자열 표현 | 예 |
| `rentalDuration` | 임대 기간(초)(기본값 - 0) | 아니요 |
| `fpExtension` | 짧은 양식 래핑 `extensionType` 과 `extensionPayload`쉼표로 구분된 문자열. 예: [...] `&fpExtension=wudo,AAAAAA==&`[..] | 아니오, 아무 번호나 사용할 수 있습니다 |

**표 5:토큰 제한 쿼리 매개 변수**

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
   <td> 이 토큰의 만료 시간입니다. 이 값은 'Z' 영역 지정자("Zulu time")의 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 날짜/시간 형식의 문자열이거나 '+' 기호 앞에 있는 정수여야 합니다. RFC 3339 날짜/시간의 예는 <span class="codeph"> 2006-04-14T12:01:10Z입니다 </span>. <p>값이 RFC 3339 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> 날짜/시간 형식의 </a> 문자열이면 토큰에 대한 절대 만료 날짜/시간을 나타냅니다. 값이 '+' 기호 앞에 있는 정수인 경우 발행부터 토큰의 유효성이 상대 시간(초)으로 해석됩니다. </p> 예를 들어 + <span class="codeph"> 60은 1분을 </span> 지정합니다. 최대 및 기본(지정되지 않은 경우) 토큰 수명은 30일입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 6:상관 관계 쿼리 매개 변수**

| **쿼리 매개 변수** | **설명** | **필수?** |
|---|---|---|
| `cookie` | 토큰에 들어 있고 토큰 상환 서버에서 로깅한 최대 32자 길이의 임의 문자열. 이 ID를 사용하여 상환 서버와 서비스 공급자의 서버에 있는 로그 항목의 상관 관계를 지정할 수 있습니다. | 아니요 |

**응답**

**표 7:HTTP 응답**

| **HTTP 상태 코드** | **설명** | **컨텐츠 유형** | **엔티티 본문 포함** |
|---|---|---|---|
| `200 OK` | 오류가 없습니다. | `text/uri-list` | 라이센스 획득 URL + 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` or `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` or `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` or `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` or `application/json` | 오류 설명 |

**표 8:이벤트 오류 코드**

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
   <td> 잘못된 토큰 만료 시간:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 잘못된 IP 주소 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 잘못된 컨텐츠 암호화 키:&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 잘못된 출력 제어 플래그가 지정되었습니다.&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 인증 토큰을 제공해야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 인증 토큰이 잘못되었습니다.&lt;details&gt; <p>참고: 인증자가 잘못되거나 제작 인증자를 사용하여 <span class="filepath"> *.test.express.com의 테스트 API에 액세스할 때 </span> 또는 그 반대로 발생할 수 있습니다. </p> <p importance="high">참고: 테스트 SDK 및 고급 테스트 도구(ATT)는 <span class="filepath"> *.test.express.com에서만 </span>작동하는 반면 프로덕션 장치에서는 <span class="filepath"> *.service.express.com을 사용해야 합니다 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 사용할 수 있는 토큰 부족 </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> 권한 유형 없음 </td> 
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
   <td> 임대 재생 기간이 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 대여 재생 기간이 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 컨텐츠 암호화 키는 32자의 16진수여야 합니다. </td> 
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
   <td> <span class="codeph"> OutputControlFlag는 4바이트를 인코딩해야 </span> 합니다. </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 잘못된 오류 형식이 지정되었습니다.&lt;format&gt; </td> 
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
   <td> 실종 아이 </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 키 저장소 서비스에서 콘텐츠 키를 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> kid </span> 는 32자의 16진수 문자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> chid </span> 는^ 뒤에 64자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 잘못된 <span class="codeph"> 자식 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 잘못된 암호화 키 또는 <span class="codeph"> 키 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 잘못된 일반 플래그 </td> 
  </tr> 
  <tr> 
   <td> -6001 </td> 
   <td> 잘못된 <span class="codeph"> FPExtension </span> 매개 변수가 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> 잘못된 FP 토큰 유형 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 잘못된 <span class="codeph"> iv </span> 매개 변수가 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> FP용 CKC를 생성하지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 잘못된 키 데이터가 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> FairPlay 지원에 대한 서비스가 인증되지 않음 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 잘못된 임대 기간이 지정되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay에서 장치 ID 바인딩이 지원되지 않음 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> FairPlay 옵션 사용 안 함 </td> 
  </tr> 
 </tbody> 
</table>