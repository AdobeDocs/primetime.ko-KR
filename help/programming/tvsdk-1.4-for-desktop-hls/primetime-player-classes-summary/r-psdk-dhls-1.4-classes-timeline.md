---
description: 이러한 클래스는 광고 배치를 포함하여 특정 미디어의 타임라인에 대한 정보를 제공합니다.
title: 타임라인 클래스
exl-id: 8382fff2-0f10-4a8c-9c0c-66d26fe18938
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 타임라인 클래스{#timeline-classes}

이러한 클래스는 광고 배치를 포함하여 특정 미디어의 타임라인에 대한 정보를 제공합니다.

패키지: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이름 </th> 
   <th colname="2" class="entry"> <p>설명 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> TVSDK 라이브러리와 통합하도록 디자인된 콘텐츠 추적 모듈을 만들려는 경우 구현해야 하는 프로토콜을 정의하는 인터페이스입니다. <p>이 인터페이스를 사용하려면 진행 이벤트가 원격 추적 시스템에 보고되는 방식을 정의해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 영업 기회 </a> </span> </td> 
   <td colname="2"> 모든 영업 기회 클래스에 대한 기본 클래스입니다. 영업 기회 클래스는 타임라인에서 "관심 있는" 지점을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 배치 </a> </span> </td> 
   <td colname="2"> 타임라인 배치와 관련된 정보를 래핑하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 배치 모드 </a> </span> </td> 
   <td colname="2"> 콘텐츠 삽입 또는 바꾸기 여부와 같은 배치 모드 열거. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> 타임라인에서 배치가 수행되는 위치를 나타내는 배치 유형 열거형(예: PRE_ROLL). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 예약 </a> </span> </td> 
   <td colname="2"> 예약은 타임라인 상의 특정 시간 범위의 추가 처리를 제한하거나 방지하기 위해 사용됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 타임라인 </a> </span> </td> 
   <td colname="2"> 타임라인 마커 처리를 위한 반복기를 제공하는 인터페이스입니다. 광고 브레이크를 포함하여 컨텐츠의 타임라인을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem </a> </span> </td> 
   <td colname="2"> 클래스. 타임라인 항목의 변경할 수 없는 일반 표현입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker </a> </span> </td> 
   <td colname="2"> 타임라인의 마커를 나타내는 클래스입니다. 이렇게 하면 실제 타임라인에서 관심 영역이 표시됩니다. 현재 관심 영역은 스크러빙 막대 UI에 다른 색상으로 표시할 수 있는 광고입니다. 각 마커는 위치 및 기간(각각 밀리초로 표현)으로 정의됩니다. </td> 
  </tr> 
 </tbody> 
</table>
