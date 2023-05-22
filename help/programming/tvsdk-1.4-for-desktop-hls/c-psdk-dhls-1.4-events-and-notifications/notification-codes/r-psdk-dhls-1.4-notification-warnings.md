---
description: 이 표는 WARN에 대한 자세한 정보를 증명합니다. 알림을 입력합니다.
title: 경고 알림 코드
exl-id: 3d76aba4-ace8-4a49-b930-96bbcad41f25
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# 경고 알림 코드{#warning-notification-codes}

이 표는 WARN에 대한 자세한 정보를 증명합니다. 알림을 입력합니다.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

대부분의 경고에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 기본 비디오 콘텐츠, 대체 오디오 콘텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함됩니다.

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
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> 찾기 오류 </span> </td> 
   <td colname="4"><span class="codeph"> 설명 </span> </td> 
   <td colname="5"> <p>재생 관련 작업이 실패했지만 재생이 계속될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 해결 중 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ 실패 </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>ad-resolver가 광고 콘텐츠를 확인/삽입하지 못했습니다. 재생이 계속될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>배경 매니페스트</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ 경고</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span> <span class="codeph"> 설명</span> </td> 
   <td colname="5"> <p> 백그라운드 매니페스트 다운로드 중 오류가 발생했습니다. 배경 매니페스트를 업데이트하는 데 문제가 있으면 TVSDK 경고로 발송되므로 재생이 중지되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_ 경고</span> </td> 
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
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_ALERT </span> </td> 
   <td colname="3" morerows="1"> <p>없음 </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_이름 </span><span class="codeph"> 설명 </span> </p> </td> 
   <td colname="5"> <p>낮은 수준의 AVE 라이브러리에서 오류가 발생했습니다. </p> <p>다음을 참조하십시오 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR 알림에 대한 세부 정보</a> 를 참조하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">DRM 부 오류 코드 및 DRM 서버 오류 문자열. 다음을 참조하십시오 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR 알림에 대한 세부 정보</a> 를 참조하십시오.
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
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ALERT </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일반 경고 이벤트를 표시합니다. 실제로 TVSDK에서 발급하지 않았습니다. 경고 이벤트에 해당하는 숫자 코드 범위의 끝에 대한 표시일 뿐입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
