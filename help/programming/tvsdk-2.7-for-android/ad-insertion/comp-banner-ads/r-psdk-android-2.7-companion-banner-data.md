---
description: AdAsset의 내용은 컴패니언 배너를 설명합니다.
title: 컴패니언 배너 데이터
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 컴패니언 배너 데이터 {#companion-banner-data}

AdAsset의 내용은 컴패니언 배너를 설명합니다.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

각 `AdAsset`은 에셋 표시에 대한 정보를 제공합니다.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 사용 가능한 정보 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 너비 </td> 
   <td colname="col2"> 컴패니언 배너의 폭(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> 컴패니언 배너의 높이(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 리소스 유형 </td> 
   <td colname="col2">이 컴패니언 배너의 리소스 유형: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:데이터는 HTML 코드에 있습니다. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:데이터는 iframe URL(src)입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 정적 URL </td> 
   <td colname="col2"> <p>경우에 따라 컴패니언 배너에는 이미지 또는 <span class="codeph"> .swf</span>(flash 배너)에 대한 직접 URL인 <span class="codeph"> staticURL</span>도 있습니다. </p> <p>html 또는 iframe을 사용하지 않으려면 이미지 또는 swf에 대한 직접 URL을 사용하여 Flash 스테이지에 배너를 표시할 수 있습니다. 이 경우 <span class="codeph"> staticURL</span>을 사용하여 배너를 표시할 수 있습니다. </p> <p>중요: 정적 URL을 유효한 문자열인지 확인해야 합니다. 이 속성을 항상 사용할 수는 없기 때문입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

