---
description: PlayReady 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
seo-description: PlayReady 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.
seo-title: 재생Ready 라이선스 토큰 요청/응답
title: 재생Ready 라이선스 토큰 요청/응답
uuid: 20ebd582-ebb9-4716-8c1e-df3e58d6ec14
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 재생Ready 라이선스 토큰 요청/응답 {#playready-license-token-request-response}

PlayReady 라이선스 토큰 인터페이스는 프로덕션 및 테스트 서비스를 제공합니다.

이 HTTP 요청은 PlayReady 라이선스로 상환할 수 있는 토큰을 반환합니다.

**방법:GET, POST** (두 메서드 모두에 대한 매개 변수가 포함된 www-url 인코딩 본문 포함)

**URL:**

* **제작:** `https://pr-gen.{prod_domain}/hms/pr/token`

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

**표 9:토큰 쿼리 매개 변수**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>쿼리 매개 변수</b> </th> 
   <th class="entry"><b>설명</b> </th> 
   <th class="entry"><b>필수</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>이는 제작 및 테스트 환경에 적합한 고객 API 키입니다. ExpressPlay 관리 대시보드 탭에서 확인할 수 있습니다. </p> </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>html <span class="codeph"> 또는</span> json <span class="codeph"></span>중 하나. html <span class="codeph"></span> (기본값)이 응답의 엔티티 본문에 오류의 HTML 표현을 제공하는 경우 <p>json <span class="codeph"> 을</span> 지정하면 JSON 형식의 구조화된 응답이 반환됩니다. 자세한 내용은 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON 오류를</a> 참조하십시오. </p> <p>응답의 MIME 유형은 성공 시 <span class="codeph"> 텍스트/uri-list</span> , HTML 오류 포맷의 <span class="codeph"> 텍스트/html</span> 또는 JSON 오류 포맷의 <span class="codeph"> application/json</span> 중 하나입니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

**표 10:라이센스 쿼리 매개 변수**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>쿼리 매개 변수</b> </th> 
   <th class="entry"><b>설명</b> </th> 
   <th class="entry"><b>필수</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>라이센스 플래그를 나타내는 4바이트 16진수 문자열입니다. 영구 라이선스는 '00000001'로 설정해야 합니다. <p>참고:임대 라이선스(<span class="codeph"> rights Type=Rental</span>)는 지속되어야 합니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> 키 암호화 키(KEK). 키는 키 래핑 알고리즘(AES Key Wrap, RFC3394)을 사용하여 KEK로 암호화되어 저장됩니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 아이</span> </td> 
   <td>컨텐츠 암호화 키 또는 문자열 ^ <span class="codeph"> somestring'의 16바이트 16진수 문자열 표현</span>. 문자열 뒤에 '^'가 오는 길이는 64자보다 길 수 없습니다. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> 암호화된 콘텐츠 키의 16진수 문자열 표현입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> 컨텐츠 암호화 키의 16바이트 16진수 문자열 표현 </td> 
   <td>예, <span class="codeph"> 키크</span> , <span class="codeph"> 에크</span> , <span class="codeph"> 아이</span> 등이제공되지 않는 한가능합니다 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>권한 종류를 지정합니다. BuyToOwn <span class="codeph"> 또는 Rental이어야</span> 합니다 <span class="codeph"></span>. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>임대 종료 날짜. 이 값은 'Z' 영역 지정자("Zulu time") 형식의 'RFC 3339' 날짜/시간 형식 또는 '+' 기호 앞에 있는 정수여야 합니다. <p>값이 RFC 3339 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> 날짜</a> /시간 형식이면 라이선스의 절대 만료 날짜/시간을 나타냅니다. RFC 3339 날짜/시간의 예는 2006-04-14T12:01:10Z입니다. </p> <p> 값이 '+' 기호 앞에 있는 정수인 경우 토큰을 발행한 시점부터 상대적인 시간(초)으로 설정됩니다. 이 시간 이후에는 콘텐츠를 재생할 수 없습니다. Rights Type이 <span class="codeph"> Rental인</span> 경우에만 <span class="codeph"> 유효합니다</span>. </p> </td> 
   <td>예, rights Type <span class="codeph"> 이</span> Rental인 <span class="codeph"> 경우</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>재생이 시작되면 컨텐츠를 재생할 수 있는 시간(초)입니다. rights Type이 <span class="codeph"> Rental인</span> 경우에만 유효합니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> 아날로그 비디오의 출력 보호 수준을 나타내는 정수 값입니다. 유효한 범위 0-999. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 압축된 디지털 오디오의 출력 보호 수준을 나타내는 정수 값입니다. 유효한 범위 0-999. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> 압축된 디지털 비디오의 출력 보호 수준을 나타내는 정수 값입니다. 유효한 범위 0-999. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> 압축되지 않은 디지털 오디오의 출력 보호 수준을 나타내는 정수 값입니다. 유효한 범위 0-999. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> 압축되지 않은 디지털 비디오의 출력 보호 수준을 나타내는 정수 값. 유효한 범위 0-999. </td> 
   <td> 예 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>출력을 알 수 없을 때 필요한 비헤이비어가 표시됩니다. 허용된 값:허용 <span class="codeph"> ,</span>허용 <span class="codeph"> 또는</span> <span class="codeph"> SDOnly</span> </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 다른 출력 제어 옵션에 대한 플래그를 나타내는 4바이트 16진수 값 </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>확장의 32비트 식별자를 나타내는 임의의 4자 단어 각 문자의 8비트 ASCII 코드는 식별자의 해당 8비트 바이트 부분입니다. 예를 들어 식별자 값 0x61626364(16진수)는 '<span class="codeph"> abcd</span>'로 기록됩니다. 'a'의 ASCII 코드는 0x61 등이기 때문입니다. </td> 
   <td> 아니요 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Extension의 base64 인코딩 문자열입니다. </td> 
   <td>예. extension <span class="codeph"> Type이</span> 지정된 경우 </td> 
  </tr> 
 </tbody> 
</table>

## 응답 {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**표 11:HTTP 응답**

| **HTTP 상태 코드** | **설명** | **컨텐츠 유형** | **엔티티 본문에 포함** |
|---|---|---|---|
| `200 OK` | 오류가 없습니다. | `text/uri-list` | 라이센스 획득 URL 및 토큰 |
| `400 Bad Request` | 잘못된 인수 | `text/html` or `application/json` | 오류 설명 |
| `401 Unauthorized` | 인증 실패 | `text/html` or `application/json` | 오류 설명 |
| `404 Not found` | 잘못된 URL | `text/html` or `application/json` | 오류 설명 |
| `50x Server Error` | 서버 오류 | `text/html` or `application/json` | 오류 설명 |

**표 12:이벤트 오류 코드**

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
   <td> 잘못된 출력 제어 플래그를 지정했습니다.&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 인증 토큰을 제공해야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td>인증 토큰이 잘못되었습니다.&lt;details&gt; <p>참고: 인증자가 잘못된 경우 또는 *.test.express.com에서 프로덕션 인증자를 사용하여 테스트 API에 액세스할 때 또는 그 반대로 발생할 수 있습니다. </p> <p importance="high">참고:Test SDK 및 Advanced Test Tool(ATT)은 <span class="filepath"> *.test.expressplay.com</span>에서만 작동하지만 프로덕션 장치는 <span class="filepath"> *.service.express.com</span>을사용해야 합니다. </p> </td> 
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
   <td> 대여 재생 기간이 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 대여 재생 기간이 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 컨텐츠 암호화 키는 32자리 16진수여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay 관리 오류:&lt;details&gt; </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> 는 4바이트를 인코딩해야 합니다. </td> 
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
   <td> -4018 </td> 
   <td>실종된 <span class="codeph"> 아이</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 키 저장소 서비스에서 콘텐츠 키를 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> kid</span> 는 32자의 16진수 문자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 어린이는</span> ^ 뒤에 오는 64자여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>잘못된 <span class="codeph"> 자식</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>잘못된 암호화 <span class="codeph"> 키</span> 또는 키 </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 알 수 없는 출력 유형 오류가 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 이 서비스에 대해 PlayReady 옵션을 사용할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 잘못된 일반 플래그 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 장치 ID는 32자의 16진수여야 합니다. </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> 잘못된 장치 ID </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> 누락된 OPL 값 </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>키 또는 <span class="codeph"> 콘텐트</span> 키 중 <span class="codeph"> 하나만</span> 지정할 수 있습니다. </td> 
  </tr> 
 </tbody> 
</table>
