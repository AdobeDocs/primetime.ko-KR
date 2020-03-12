---
description: 이러한 클래스는 광고 배치를 포함하여 특정 미디어의 타임라인에 대한 정보를 제공합니다.
seo-description: 이러한 클래스는 광고 배치를 포함하여 특정 미디어의 타임라인에 대한 정보를 제공합니다.
seo-title: 타임라인 클래스
title: 타임라인 클래스
uuid: 9c06fec1-d725-4fe8-9cf5-1e3ade2b7d27
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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
   <td colname="1"> <span class="codeph"> 컨텐츠 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> 추적기 </a></span> </td> 
   <td colname="2"> TVSDK 라이브러리와 통합되도록 설계된 컨텐츠 추적 모듈을 만들려면 구현해야 하는 프로토콜을 정의하는 인터페이스입니다. <p>이 인터페이스를 사용하려면 진행률 이벤트가 원격 추적 시스템에 보고되는 방식을 정의해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 영업 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 기회 </a></span> </td> 
   <td colname="2"> 모든 기회 클래스에 대한 기본 클래스입니다. 기회 클래스는 타임라인에서 "관심" 점을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 배치 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"></a></span> </td> 
   <td colname="2"> 타임라인 배치와 관련된 정보를 래핑하는 클래스입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 배치 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 모드 </a></span> </td> 
   <td colname="2"> 컨텐츠 삽입 또는 바꾸기 여부와 같은 배치 모드 열거형입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 배치 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> 유형 </a></span> </td> 
   <td colname="2"> 타임라인에서 배치가 수행되는 위치를 나타내는 배치 유형 열거형예: PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 예약 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"></a></span> </td> 
   <td colname="2"> 예약은 타임라인에서 특정 시간 범위의 추가 처리를 제한하거나 방지하는 데 사용됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 타임라인 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"></a></span> </td> 
   <td colname="2"> 타임라인 마커 처리를 위한 반복기를 제공하는 인터페이스입니다. 광고 분리를 포함하여 컨텐츠의 타임라인을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 타임라인 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 항목 </a></span> </td> 
   <td colname="2"> 수업. 타임라인 항목의 일반 변경 불가능한 표현. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 타임라인 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 마커 </a></span> </td> 
   <td colname="2"> 타임라인에서 마커를 나타내는 클래스입니다. 이것은 실제 타임라인에 대한 관심 영역을 표시합니다. 현재 관심 영역은 광고로, 예를 들어 스크러빙 막대 UI에 다른 색상으로 표시할 수 있습니다. 각 마커는 위치와 지속 시간(각각 밀리초 단위)으로 정의됩니다. </td> 
  </tr> 
 </tbody> 
</table>

