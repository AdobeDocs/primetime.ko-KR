---
description: TVSDK 알림 시스템에서는 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
title: 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 알림 코드 {#notification-codes}

TVSDK 알림 시스템에서는 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 객체는 플레이어 상태와 관련된 정보를 제공합니다. TVSDK는 알림 객체의 시간순으로 정렬된 목록을 제공합니다. 각 알림에는 다음 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 요소</b></th> 
   <th colname="2" class="entry"><b> 설명</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>알림 유형입니다. </p> <p>플랫폼에 따라 이 속성은 INFO, WARN 및 ERROR 값이 가능한 열거형 유형입니다. 알림을 위한 최상위 수준의 그룹입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>다음 숫자 표현들이 알림에 지정됩니다. 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">오류 알림 이벤트(10000~199999) </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">경고 알림 이벤트(20000~299999) </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">정보 알림 이벤트(30000~399999) </li> 
     </ul> </p> <p>오류와 같은 각 최상위 수준 범위는 재생 오류를 나타내는 101000~101999와 같은 하위 범위로 분할됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR</span>과 같이 사용자가 읽을 수 있는 알림 이벤트에 대한 설명을 포함하는 문자열입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 메타데이터</span> </td> 
   <td colname="2"> <p>알림에 대한 추가 관련 정보가 들어 있는 키/값 쌍. </p> <p>예를 들어 <span class="codeph"> URL</span>이라는 키는 오류를 일으킨 잘못된 URL과 같이 알림과 관련된 URL인 값을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>이 알림에 직접 영향을 준 다른 <span class="codeph"> MediaPlayerNotification</span> 개체에 대한 참조입니다. </p> <p>한 예로 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림일 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>