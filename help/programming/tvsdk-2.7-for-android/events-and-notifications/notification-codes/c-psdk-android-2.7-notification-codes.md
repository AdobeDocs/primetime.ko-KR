---
description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
title: 알림 코드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 개요 {#notification-codes-overview}

TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 개체는 플레이어의 상태와 관련된 정보를 제공합니다. TVSDK는 시간순으로 정렬된 알림 개체 목록을 제공합니다. 각 알림에는 다음 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 요소 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 유형</span> </td> 
   <td colname="2"> <p>알림 유형. </p> <p>이 속성은 플랫폼에 따라 INFO, WARN 및 ERROR 값이 가능한 열거형 유형입니다. 알림의 최상위 그룹입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 코드</span> </td> 
   <td colname="2"> <p>다음 숫자 표현이 알림에 지정됩니다. 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">오류 알림 이벤트(100000~199999) </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">경고 알림 이벤트(200000~299999) </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">300000부터 399999까지 정보 알림 이벤트 </li> 
     </ul> </p> <p>오류와 같은 각 최상위 범위는 재생 오류를 나타내는 101000~101999과 같은 하위 범위로 구분됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 이름</span> </td> 
   <td colname="2">사람이 인식할 수 있는 알림 이벤트 설명이 포함된 문자열(예: ) <span class="codeph"> 찾기 오류</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 메타데이터</span> </td> 
   <td colname="2"> <p>알림에 대한 추가 관련 정보가 포함된 키/값 쌍입니다. </p> <p>예를 들어 <span class="codeph"> URL</span> 은 오류를 일으킨 잘못된 URL과 같이, 알림과 관련된 URL인 값을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>다른 참조에 대한 참조 <span class="codeph"> MediaPlayerNotification</span> 이 알림에 직접적인 영향을 준 오브젝트. </p> <p>한 가지 예는 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림일 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
