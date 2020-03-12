---
description: TVSDK 플레이어는 이벤트를 전달하여 사용자 지정 광고 로드 상태를 표시하거나 로드하는 데 너무 오래 걸리거나 오류가 있는 광고를 무시합니다. 이러한 이벤트는 events.CustomAdEvents에서 정의됩니다.
seo-description: TVSDK 플레이어는 이벤트를 전달하여 사용자 지정 광고 로드 상태를 표시하거나 로드하는 데 너무 오래 걸리거나 오류가 있는 광고를 무시합니다. 이러한 이벤트는 events.CustomAdEvents에서 정의됩니다.
seo-title: 사용자 지정 광고 이벤트
title: 사용자 지정 광고 이벤트
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> 뷰어가 사용자 지정 광고를 클릭한 횟수입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> 사용자 지정 광고에 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 로드되었습니다.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> 사용자 지정 광고를 로드하는 중입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 일시 중지됨 </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 일시 중지되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> 일시 중지 후 사용자 지정 광고 재생이 계속되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 광고 재생 </span> </td> 
   <td colname="col2"> 사용자 지정 광고가 재생되고 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>사용자 지정 광고 플레이어는 TVSDK 플레이어에 사용자 지정 광고의 진행 상태를 알립니다. &amp;nbsp; </p> <p>이 <span class="codeph"> 이벤트와 함께 </span> 광고의 현재 시간 및 <span class="codeph"> 총 </span> 시간이 전달됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> 사용자 지정 광고 재생이 시작되어 뷰어에 표시됩니다.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 광고 중지됨 </td> 
   <td colname="col2"> 사용자 지정 광고 재생이 완료되었습니다. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

