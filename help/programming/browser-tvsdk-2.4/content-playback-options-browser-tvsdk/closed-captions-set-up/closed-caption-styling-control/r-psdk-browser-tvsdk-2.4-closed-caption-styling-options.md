---
description: 여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원본 캡션의 스타일 옵션을 덮어씁니다.
seo-description: 여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원본 캡션의 스타일 옵션을 덮어씁니다.
seo-title: 닫힌 캡션 스타일 옵션
title: 닫힌 캡션 스타일 옵션
uuid: 0e2fd9f3-e569-4b5d-9b78-86f8ee6230ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 닫힌 캡션 스타일 옵션{#closed-caption-styling-options}

여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원본 캡션의 스타일 옵션을 덮어씁니다.

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
>기본값(예: `DEFAULT`)을 정의하는 옵션에서 해당 값은 캡션이 원래 지정된 시점을 나타냅니다.

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
   <td colname="2"> <p>글꼴 유형입니다. </p> <p><span class="codeph"> TextFormat.Font </span> 열거형으로 정의된 값으로만 설정할 수 있으며 serifs를 포함하거나 포함하지 않고 고정 간격(예: )을 나타냅니다. </p> <p>팁: 장치에서 사용할 수 있는 실제 글꼴은 다를 수 있으며 필요한 경우 대체 글꼴을 사용합니다. 이 대체는 시스템별로 지정할 수 있지만, serifs가 있는 고정 공간은 일반적으로 대용으로 사용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 크기 </td> 
   <td colname="2"> <p>캡션의 크기입니다. </p> <p> <span class="codeph"> TextFormat.Size </span> 열거에 의해 정의된 값만 설정할 수 있습니다. 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 중간  </span> - 표준 크기 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE  </span> - 중간 크기보다 약 30% 큼 </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 소형  </span> - 중간 크기보다 약 30% 작음 </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT  </span> - 캡션의 기본 크기입니다.미디어와 동일 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 색상 </td> 
   <td colname="2"> <p>글꼴 색상 </p> <p><span class="codeph"> TextFormat.Color </span> 열거에 의해 정의된 값만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경색 </td> 
   <td colname="2"> <p>배경 문자 색상. </p> <p>글꼴 색상에 사용할 수 있는 값만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 불투명도 </td> 
   <td colname="2"> <p>텍스트의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 글꼴의 DEFAULT_OPACITY </span> 는 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 아래쪽 인세트 </td> 
   <td colname="2"> <p>캡션을 피하려면 캡션 창 아래쪽에서 세로 거리입니다. </p> <p>캡션 창 높이(예: "20%") 또는 픽셀 수(예: "20")로 표현됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 안전 영역 </td> 
   <td colname="2"> <p>0%에서 25% 사이의 화면 가장자리 주변에 캡션이 표시되지 않는 영역입니다. </p> <p>기본적으로 608/708의 안전 영역은 12%이고 WebVTT의 안전 영역은 0%입니다. 이 설정을 사용하면 응용 프로그램이 해당 기본값을 무시할 수 있습니다. 예를 들어 "10%,20%" 문자열을 제공하는 경우 첫 번째 값은 수평 보호 영역이고 두 번째 값은 수직 안전 영역입니다. 예를 들어 문자열 "15%"와 같은 하나의 값이 제공되면 세로 축과 가로 축에서 모두 지정된 안전 영역을 사용합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

