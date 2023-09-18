---
description: SEES와 협력하여 ExpressPlay를 사용하여 시간 기반 권리 유형 서비스를 활성화하는 방법을 알아보십시오.
title: 참조 서비스 시간 기반 권한
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 참조 서비스: 시간 기반 권한 {#reference-service-time-based-entitlement}

SEES와 협력하여 ExpressPlay를 사용하여 시간 기반 권리 유형 서비스를 활성화하는 방법을 알아보십시오.

SEES는 클라이언트로부터 자격 요청(공개 API 섹션 참조)을 수신합니다. SEES 서버는 `contentID`을(를) 추가하고 `expirationTime`를 누르고 ExpressPlay 서버에 요청을 전달합니다. 최종 ExpressPlay 토큰은 시간이 제한됩니다. 아래의 시간 기반 자격 시퀀스 다이어그램을 참조하십시오. ![](assets/fees-time-based.png)

**표 1: 클라이언트가 보낸 라이선스 매개 변수**

| 쿼리 매개 변수 | 설명 | 필수 |
|---|---|---|
| `contentKey` | 콘텐츠 암호화 키의 16바이트 16진수 문자열 표현 | 예 |
| `iv` | 콘텐츠 암호화 IV의 16바이트 16진수 문자열 표현 | 예 |
| `rentalDuration` | 임대 기간(초)(기본값 = 0) | 아니요 |

**표 2: SEES 서버에서 추가한 토큰 제한 매개 변수**

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
   <td>이 토큰의 만료 시간. 이 값은 의 문자열이어야 합니다. <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> 'Z' 영역 지정자의 날짜/시간 형식("Zulu time") 또는 앞에 '+' 기호가 있는 정수 RFC 3339 날짜/시간의 예는 다음과 같습니다. <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>값이 RFC 3339 날짜/시간 형식의 문자열인 경우 토큰의 절대 만료 날짜/시간을 나타냅니다. 값이 앞에 '+' 기호가 있는 정수인 경우 토큰이 유효하다는 발급의 상대적 시간(초)으로 해석됩니다. 예를 들어, <span class="codeph"> +60</span> 1분을 지정합니다. 최대(및 지정하지 않은 경우 기본값) 토큰 수명은 30일입니다. '+' 기호를 지정할 때 인코딩된 양식 "%2B"을(를) 사용하십시오. </p> </td> 
   <td> 아니요 </td> 
  </tr> 
 </tbody> 
</table>
