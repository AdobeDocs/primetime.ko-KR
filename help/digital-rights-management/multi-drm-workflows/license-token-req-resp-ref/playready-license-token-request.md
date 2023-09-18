---
description: PlayReady 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
title: PlayReady 라이선스 토큰 요청/응답
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# PlayReady 라이선스 토큰 요청/응답 {#playready-license-token-request-response}

PlayReady 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.

이 HTTP 요청은 PlayReady 라이선스에 대해 상환할 수 있는 토큰을 반환합니다.

**방법: GET, POST** (두 메서드의 매개 변수가 포함된 www-url로 인코딩된 본문 사용)

**URL:**

* **프로덕션:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **테스트:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **샘플 요청:**

  ```
  <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
   <ExpressPlay customer authenticator identifier>
   &kid=<CEKSID>
   &contentKey=<CEK>
   &rightsType=BuyToOwn
   &analogVideoOPL=0
   &compressedDigitalAudioOPL=0
   &compressedDigitalVideoOPL=0
   &uncompressedDigitalAudioOPL=0
   &uncompressedDigitalVideoOPL=0
  </xref href="https:>
  ```

* **샘플 응답:**

  ```
  {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
              "token":"<base64-encoded ExpressPlay token>"}
  ```

## 요청 쿼리 매개 변수 {#section_26F8856641A64A46A3290DBE61ACFAD2}

**표 9: 토큰 쿼리 매개 변수**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>쿼리 매개 변수</b> </th> 
   <th class="entry"><b>설명</b> </th> 
   <th class="entry"><b>필수?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>프로덕션 및 테스트 환경에 대해 각각 하나씩 제공되는 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 찾을 수 있습니다. </p> </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>다음 중 하나 <span class="codeph"> html</span> 또는 <span class="codeph"> json</span>. If <span class="codeph"> html</span> (기본값) 모든 오류의 HTML 표현은 응답의 엔티티 본문에서 제공됩니다. <p>If <span class="codeph"> json</span> 을 지정하면 JSON 형식의 구조화된 응답이 반환됩니다. 다음을 참조하십시오 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON 오류</a> 을 참조하십시오. </p> <p>응답의 mime 유형은 다음 중 하나입니다. <span class="codeph"> text/uri-list</span> 성공 시, <span class="codeph"> text/html</span> HTML 오류 형식용 또는 <span class="codeph"> application/json</span> JSON 오류 형식용 </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 10: 라이선스 쿼리 매개 변수**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>쿼리 매개 변수</b> </th> 
   <th class="entry"><b>설명</b> </th> 
   <th class="entry"><b>필수?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>라이선스 플래그를 나타내는 4바이트의 16진수 문자열입니다. 영구 라이센스의 경우 '00000001'로 설정해야 합니다. <p>참고: 임대 라이선스 (<span class="codeph"> rightsType=Rental</span>)은 영구적이어야 합니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 케크</span> </td> 
   <td> 키 암호화 키(KEK). 키는 키 래핑 알고리즘(AES Key Wrap, RFC3394)을 사용하여 KEK로 암호화되어 저장됩니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 아이</span> </td> 
   <td>콘텐츠 암호화 키 또는 문자열의 16바이트 16진수 문자열 표현 <span class="codeph"> ^somestring'</span>. 문자열 뒤에 '^'가 오는 길이는 64자를 초과할 수 없습니다. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> 암호화된 콘텐츠 키의 16진수 문자열 표현입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> 콘텐츠 암호화 키의 16바이트 16진수 문자열 표현 </td> 
   <td>예, 그렇지 않으면 <span class="codeph"> 케크</span> 및 <span class="codeph"> ek</span> 또는 <span class="codeph"> 아이</span> 제공됨 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>권한의 종류를 지정합니다. 은(는) 이어야 합니다. <span class="codeph"> BuyToOwn</span> 또는 <span class="codeph"> 임대</span>. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>대여 종료일. 이 값은 'Z' 영역 지정자('Zulu time') 형식의 'RFC 3339' _ 날짜/시간 형식이거나 '+' 기호가 앞에 오는 정수여야 합니다. <p>값이 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> 날짜/시간 형식인 경우에는 라이센스의 절대 만료 날짜/시간을 나타냅니다. RFC 3339 날짜/시간의 예는 2006-04-14T12입니다.:01:10Z </p> <p> 값이 앞에 '+' 기호가 있는 정수인 경우 토큰을 발급한 시점부터 상대적 시간(초)으로 간주됩니다. 이 시간 이후에는 콘텐츠를 재생할 수 없습니다. 다음과 같은 경우에만 유효합니다. <span class="codeph"> rightsType</span> 은(는) <span class="codeph"> 임대</span>. </p> </td> 
   <td>예, 다음과 같은 경우: <span class="codeph"> rightsType</span> 은(는) <span class="codeph"> 임대</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>재생이 시작된 후 콘텐츠를 재생할 수 있는 시간(초)입니다. 다음과 같은 경우에만 유효합니다. <span class="codeph"> rightsType</span> 렌탈입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 아날로그 비디오 OPL</span> </td> 
   <td> 아날로그 비디오의 출력 보호 수준을 나타내는 정수 값입니다. 0-999의 유효 범위. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 압축된 디지털 오디오의 출력 보호 수준을 나타내는 정수 값입니다. 0-999의 유효 범위. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 압축된 디지털 비디오 OPL</span> </td> 
   <td> 압축된 디지털 비디오의 출력 보호 수준을 나타내는 정수 값입니다. 0-999의 유효 범위. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 압축되지 않은 디지털 오디오 OPL</span> </td> 
   <td> 압축되지 않은 디지털 오디오의 출력 보호 수준을 나타내는 정수 값입니다. 0-999의 유효 범위. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> 압축되지 않은 디지털 비디오의 출력 보호 수준을 나타내는 정수 값입니다. 0-999의 유효 범위. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 알 수 없는 출력 동작</span> </td> 
   <td>출력을 알 수 없는 경우 필요한 동작입니다. 허용되는 값: <span class="codeph"> 허용</span>, <span class="codeph"> 허용 안 함</span> 또는 <span class="codeph"> SDOnly</span> </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlag</span> </td> 
   <td> 다른 출력 제어 옵션에 대한 플래그를 나타내는 4바이트의 16진수 값입니다 </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>확장에 대한 32비트 식별자를 나타내는 임의의 4자리 단어입니다. 각 문자의 8비트 ASCII 코드는 식별자의 해당 8비트 바이트 부분입니다. 예를 들어 식별자 값 0x61626364(16진수)은 '<span class="codeph"> abcd</span>', 'a'에 대한 ASCII 코드가 0x61이므로, </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> 확장의 base64 인코딩 문자열입니다. </td> 
   <td>예, 다음과 같은 경우: <span class="codeph"> extensionType</span> 이(가) 지정되었습니다. </td> 
  </tr> 
 </tbody> 
</table>

## 응답 {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**표 11: HTTP 응답**

| **HTTP 상태 코드** | **설명** | **Content-Type** | **엔티티 본문이 다음을 포함** |
|---|---|---|---|
| `200 OK` | 오류 없음. | `text/uri-list` | 라이선스 획득 URL 및 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` 또는 `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` 또는 `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` 또는 `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` 또는 `application/json` | 오류 설명 |

**표 12: 이벤트 오류 코드**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>코드</b> </th> 
   <th class="entry"><b>설명</b> </th> 
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
   <td>잘못된 인증 토큰: &lt;details&gt; <p>참고: 인증자가 잘못되었거나 프로덕션 인증자를 사용하여 *.test.expressplay.com에서 테스트 API에 액세스하거나 그 반대의 경우 이 문제가 발생할 수 있습니다. </p> <p importance="high">참고: SDK 및 ATT(고급 테스트 도구)는 <span class="filepath"> *.test.expressplay.com</span>, 반면에 프로덕션 디바이스는 <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> 은(는) 인코딩해야 합니다 4바이트 </td> 
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
   <td> -4018 </td> 
   <td>누락 <span class="codeph"> 아이</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 키 저장소 서비스에서 콘텐츠 키를 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> 아이</span> 은(는) 32개의 16진수 문자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 아이</span> ^ 뒤에 64자가 있어야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>잘못됨 <span class="codeph"> 아이</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>잘못된 암호화 <span class="codeph"> key</span> 또는 kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 알 수 없는 잘못된 출력 유형 오류 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 이 서비스에 대해 PlayReady 옵션이 비활성화되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 잘못된 일반 플래그 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 장치 ID는 32개의 16진수 문자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> 잘못된 장치 ID </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> OPL 값 누락 </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>다음 중 하나만 <span class="codeph"> 케크</span> 또는 <span class="codeph"> contentKey</span> 을(를) 지정할 수 있습니다 </td> 
  </tr> 
 </tbody> 
</table>
