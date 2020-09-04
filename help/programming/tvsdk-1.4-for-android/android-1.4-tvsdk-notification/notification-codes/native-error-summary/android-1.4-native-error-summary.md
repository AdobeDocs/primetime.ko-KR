---
seo-title: NATIVE_ERROR 알림에 대한 세부 사항
title: NATIVE_ERROR 알림에 대한 세부 사항
uuid: 18c4da57-59de-41a8-a2ea-fef800565207
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# NATIVE_ERROR 알림에 대한 세부 사항 {#details-for-the-native-error-notification}

TVSDK가 기본 오류를 처리하면 다음 메타데이터 키 값의 일부 또는 전체를 설정합니다.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 메타데이터 키 이름 </th> 
   <th colname="col2" class="entry"> 메타데이터 값 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      AVE의 기본 오류 코드입니다. 
    </pre> 이러한 코드는 다음과 같습니다. 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM 오류(코드 3300 - 3367). 이는 동등한 Flash Player 오류 코드와 동일합니다. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">비디오 재생 오류(-1 ~ 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">암호화 오류(300~307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> 오류 이름이 포함된 문자열;예: <span class="codeph"> AAXS_InvalidVoucher </span> 또는 <span class="codeph"> DECODER_FAILED </span> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> DRM 오류의 경우 하위 오류 코드도 반환됩니다. 이러한 코드는 Flash Player에서 반환되는 <span class="codeph"> DRMErrorEvents </span> 하위 오류 코드에 해당합니다. Adobe에 오류를 보고할 때 문제 해결 지원을 위해 이 숫자 값을 포함시키십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> DRM의 경우 DRM 서버 배포의 사용자 지정 오류 문자열입니다(정의된 경우). Adobe에 오류를 보고할 때도 이 항목을 포함합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 설명 </span> </td> 
   <td colname="col2"> 오류에 대한 문자열 설명입니다. 일반적으로 미디어의 URL입니다. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK는 비디오 엔진으로부터 이러한 오류 코드와 문자열을 수신합니다.

>[!IMPORTANT]
>
>Adobe Primetime DRM 클라이언트 오류 코드의 전체 목록은 [DRM 클라이언트 오류 메시지 참조를 참조하십시오](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).