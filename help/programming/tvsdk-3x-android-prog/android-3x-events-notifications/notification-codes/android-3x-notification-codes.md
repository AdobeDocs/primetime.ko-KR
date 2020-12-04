---
description: TVSDK 알림 시스템에서는 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-description: TVSDK 알림 시스템에서는 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-title: 알림 코드
title: 알림 코드
uuid: 6babb203-b6d4-4b11-9fae-41e7db7fd570
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# 알림 코드 {#notification-codes}

TVSDK 알림 시스템에서는 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 개체는 플레이어의 상태와 관련된 정보를 제공합니다. TVSDK는 시간순으로 정렬된 알림 객체 목록을 제공합니다. 각 알림에는 다음 메타데이터가 포함됩니다.

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
   <td colname="2"> <p>알림 유형입니다. </p> <p>플랫폼에 따라 이 속성은 INFO, WARN 및 ERROR의 가능한 값을 가진 열거형 유형입니다. 알림을 위한 최상위 그룹입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 코드</span> </td> 
   <td colname="2"> <p>알림에 다음 숫자 표현이 할당됩니다. 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">오류 알림 이벤트(10000~19999) </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">경고 알림 이벤트(2000~29999) </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">정보 알림 이벤트(30000~39999) </li> 
     </ul> </p> <p>오류와 같은 각 최상위 수준 범위는 재생 오류를 나타내는 101000부터 101999까지의 하위 범위로 나누어집니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">사용자가 읽을 수 있는 알림 이벤트 설명(예: <span class="codeph"> SEEK_ERROR</span>)을 포함하는 문자열. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 메타데이터</span> </td> 
   <td colname="2"> <p>알림에 대한 추가 관련 정보가 들어 있는 키/값 쌍입니다. </p> <p>예를 들어 <span class="codeph"> URL</span>이라는 키는 오류를 일으킨 잘못된 URL과 같이 알림과 관련된 URL인 값을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>이 알림에 직접 영향을 준 다른 <span class="codeph"> MediaPlayerNotification</span> 개체에 대한 참조입니다. </p> <p>한 예로, 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림일 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>