---
description: AdAsset의 콘텐츠는 컴패니언 배너에 대해 설명합니다.
title: 컴패니언 배너 데이터
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 컴패니언 배너 데이터 {#companion-banner-data}

AdAsset의 콘텐츠는 컴패니언 배너에 대해 설명합니다.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

각 `AdAsset` 에셋 표시에 대한 정보를 제공합니다.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>사용 가능한 정보 </b></th> 
   <th colname="col2" class="entry"> <b>설명</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 폭 </td> 
   <td colname="col2"> 컴패니언 배너의 픽셀 단위 폭입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 높이 </td> 
   <td colname="col2"> 컴패니언 배너의 픽셀 단위 높이입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 리소스 유형 </td> 
   <td colname="col2">이 컴패니언 배너의 리소스 유형: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: 데이터가 HTML 코드에 있습니다. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: 데이터가 iframe URL(src)입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 정적 URL </td> 
   <td colname="col2"> <p>때로는 컴패니언 배너에도 <span class="codeph"> staticURL</span> 이미지 또는 의 직접 URL입니다 <span class="codeph"> .swf</span> (Flash 배너). </p> <p>html 또는 iframe을 사용하지 않으려면 이미지나 swf에 대한 직접 URL을 사용하여 Flash 단계에 배너를 대신 표시할 수 있습니다. 이 경우 <span class="codeph"> staticURL</span> 배너를 표시합니다. </p> <p>중요: 이 속성을 항상 사용할 수 있는 것은 아니므로 정적 URL이 유효한 문자열인지 확인해야 합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
