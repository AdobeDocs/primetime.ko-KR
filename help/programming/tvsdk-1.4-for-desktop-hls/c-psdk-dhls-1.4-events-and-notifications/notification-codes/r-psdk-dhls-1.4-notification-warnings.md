---
description: 이 표에서는 WARN에 대한 자세한 정보를 보여 줍니다. 유형 알림을 참조하십시오.
title: 경고 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---


# 경고 알림 코드{#warning-notification-codes}

이 표에서는 WARN에 대한 자세한 정보를 보여 줍니다. 유형 알림을 참조하십시오.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

대부분의 경고에는 다운로드하지 못한 리소스의 URL과 같이 관련 메타데이터가 포함되어 있습니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 코드 </th> 
   <th colname="2" class="entry"> 이름 </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> 메타데이터 키 </th> 
   <th colname="5" class="entry"> 댓글 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>재생</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 200000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR  </span><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> 설명  </span> </td> 
   <td colname="5"> <p>재생 관련 작업이 실패했지만 재생이 계속될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 해결  </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL  </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED  </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID  </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>광고 확인자가 광고 콘텐츠를 확인/삽입하지 못했습니다. 재생이 계속될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>배경 매니페스트</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_경고</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> NAME 설명</span> </td> 
   <td colname="5"> <p> 백그라운드 매니페스트 다운로드에 오류가 있습니다. 배경 매니페스트를 업데이트할 때 TV SDK 경고로 전달되고 재생이 중지되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001년  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 설명</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>기본</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100  </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING  </span> </td> 
   <td colname="3" morerows="1"> <p>없음 </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> NATIVE_ERROR_NAME  </span><span class="codeph"> 설명  </span> </p> </td> 
   <td colname="5"> <p>하위 수준 AVE 라이브러리에서 오류가 발생했습니다. </p> <p>이러한 메타데이터 필드의 값에 대한 자세한 내용은 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR 알림</a>에 대한 세부 정보를 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_</span> <span class="codeph"> CODEDRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">DRM 부 오류 코드 및 DRM 서버 오류 문자열. 이러한 메타데이터 필드의 값에 대한 자세한 내용은 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR 알림</a>에 대한 세부 정보를 참조하십시오.
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>일반</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일반 경고 이벤트를 표시합니다. 실제로 TVSDK에서 발행되지 않습니다. 경고 이벤트에 해당하는 숫자 코드 범위의 끝에 대한 표시자에 불과합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

