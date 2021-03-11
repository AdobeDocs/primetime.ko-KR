---
description: TVSDK 플레이어는 이벤트를 전달하여 사용자 지정 광고 로드 상태를 표시하거나 로드하는 데 너무 오래 걸리거나 오류가 있는 광고를 무시합니다. 이러한 이벤트는 events.CustomAdEvents에서 정의됩니다.
title: 사용자 지정 광고 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# 사용자 지정 광고 이벤트{#custom-ad-events}

TVSDK 플레이어는 이벤트를 전달하여 사용자 지정 광고 로드 상태를 표시하거나 로드하는 데 너무 오래 걸리거나 오류가 있는 광고를 무시합니다. 이러한 이벤트는 events.CustomAdEvents에서 정의됩니다.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 이벤트 </th> 
   <th colname="col2" class="entry"> 정의 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru  </span> </td> 
   <td colname="col2"> 뷰어가 사용자 정의 광고를 클릭한 횟수입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError  </span> </td> 
   <td colname="col2"> 사용자 지정 광고에 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 로드되었습니다.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading  </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 로드되고 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 일시 중지되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed  </span> </td> 
   <td colname="col2"> 일시 중지 후에도 사용자 지정 광고 재생이 계속되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying  </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 재생되고 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>사용자 지정 광고 플레이어는 사용자 지정 광고의 진행 상황을 TVSDK 플레이어에 알립니다. &amp;nbsp; </p> <p>광고의 <span class="codeph"> currentTime </span> 및 <span class="codeph"> totalTime </span>이 이 이벤트와 함께 전달됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> 사용자 정의 광고 재생이 시작되어 뷰어에 표시됩니다.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> 사용자 지정 광고 재생이 완료되었습니다. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

