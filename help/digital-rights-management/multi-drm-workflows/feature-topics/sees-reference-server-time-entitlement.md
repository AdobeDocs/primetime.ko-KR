---
description: SEES를 사용하여 ExpressPlay를 사용하여 시간 기반의 권한 부여 서비스를 활성화하는 방법을 확인합니다.
title: 참조 서비스 시간 기반 권한
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 참조 서비스:시간 기반 자격 부여 {#reference-service-time-based-entitlement}

SEES를 사용하여 ExpressPlay를 사용하여 시간 기반의 권한 부여 서비스를 활성화하는 방법을 확인합니다.

SEES는 클라이언트로부터 권한 부여 요청(공개 API 섹션 참조)을 받습니다. SEES 서버는 `contentID`을 기반으로 CEK 및 IV를 검색하고, `expirationTime`을 추가하고, 요청을 ExpressPlay 서버로 전달합니다. 최종 ExpressPlay 토큰은 시간 제한이 있습니다. 아래의 시간 기반 자격 부여 시퀀스 다이어그램을 참조하십시오.![](assets/fees-time-based.png)

**표 1:클라이언트가 보낸 라이센스 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수 |
|---|---|---|
| `contentKey` | 컨텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예 |
| `iv` | 컨텐츠 암호화 IV의 16바이트 16진수 문자열 표현 | 예 |
| `rentalDuration` | 대여 기간(초)(기본값 = 0) | 아니요 |

**표 2:SEES 서버에 의해 추가된 토큰 제한 매개 변수**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 쿼리 매개 변수 </th> 
   <th class="entry"> 설명 </th> 
   <th class="entry"> 필수? </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>이 토큰의 만료 시간입니다. 이 값은 'Z' 영역 지정자("Zulu time")에 있는 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 339</a> 날짜/시간 형식의 문자열이거나 '+' 기호 앞에 오는 정수여야 합니다. RFC 3339 날짜/시간의 예는 <span class="codeph"> 2006-04-14T12:01:10Z</span>입니다. <p>값이 RFC 3339 날짜/시간 형식의 문자열이면 토큰에 대한 절대 만료 날짜/시간을 나타냅니다. 값이 '+' 기호 앞에 오는 정수인 경우, 토큰은 유효하다는 점을 발급 후 상대 시간(초)으로 해석됩니다. 예를 들어 <span class="codeph"> +60</span>은 1분을 지정합니다. 최대(및 지정되지 않은 경우 기본값) 토큰 수명은 30일입니다. '+' 기호를 지정할 때 인코딩된 양식 "%2B"을 사용합니다. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>

