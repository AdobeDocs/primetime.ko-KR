---
description: 여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원래 캡션의 스타일 옵션을 재정의합니다.
title: 선택 캡션 스타일 옵션
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 선택 캡션 스타일 옵션{#closed-caption-styling-options}

여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원래 캡션의 스타일 옵션을 재정의합니다.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>기본값을 정의하는 옵션(예: `DEFAULT`)에서 해당 값은 캡션이 원래 지정되었을 때의 설정을 나타냅니다.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 형식 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 </td> 
   <td colname="2"> <p>글꼴 유형입니다. </p> <p>에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Font </span> 열거형이며 예를 들어 serifs가 있거나 없는 단일 간격을 나타냅니다. </p> <p>팁: 디바이스에서 사용할 수 있는 실제 글꼴은 다를 수 있으며, 필요한 경우 대체 글꼴이 사용됩니다. Serifs가 있는 Monospace는 일반적으로 대체물로 사용되지만, 이 대체물은 시스템에 따라 다를 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 크기 </td> 
   <td colname="2"> <p>캡션 크기입니다. </p> <p> 에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Size </span> 열거형: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 중간 </span> - 표준 크기 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 큼 </span> - 보통 대비 약 30% 큼 </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 작음 </span> - 보통 대비 약 30% 작음 </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 기본값 </span> - 캡션의 기본 크기이며, 중간과 동일 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 색상 </td> 
   <td colname="2"> <p>글꼴 색상입니다. </p> <p>에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Color </span> 열거형입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경색 </td> 
   <td colname="2"> <p>배경 문자 셀 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값으로만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 불투명도 </td> 
   <td colname="2"> <p>텍스트의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전 불투명)까지의 백분율로 표시됩니다. <span class="codeph"> DEFAULT_불투명도 </span> 글꼴은 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 하단 삽입 </td> 
   <td colname="2"> <p>캡션을 피하기 위한 캡션 창 아래쪽으로부터의 세로 거리입니다. </p> <p>캡션 창 높이의 백분율(예: "20%") 또는 픽셀 수(예: "20")로 표시됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 안전 지역 </td> 
   <td colname="2"> <p>화면 가장자리 주변의 0%에서 25% 사이의 영역으로서, 캡션이 표시되지 않습니다. </p> <p>기본적으로 608/708의 안전 영역은 12%이고 WebVTT의 안전 영역은 0%입니다. 이 설정을 사용하면 응용 프로그램에서 해당 기본값을 재정의할 수 있습니다. 문자열 "10%,20%"와 같이 두 개의 값이 제공된 경우 첫 번째 값은 수평 안전 영역이고 두 번째 값은 수직 안전 영역이다. 문자열 "15%"와 같이 하나의 값이 제공되면 세로 및 가로 축 모두 지정된 안전 영역을 사용합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
