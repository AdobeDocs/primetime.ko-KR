---
description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-title: 알림 코드
title: 알림 코드
uuid: 24476204-5c35-4ff9-810d-77698ea18b53
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 개요 {#notification-codes-overview}

TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 개체는 플레이어의 상태와 관련된 정보를 제공합니다. TVSDK 파섹 각 알림에는 다음 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 요소 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>알림 유형입니다. </p> <p>플랫폼에 따라 이 속성은 INFO, WARN 및 ERROR 값이 가능한 열거형 유형입니다. 알림을 위한 최상위 수준의 그룹화입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>다음 숫자 표현이 알림에 지정됩니다. 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">오류 알림 이벤트(100000~19999) </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">경고 알림 이벤트(20000~29999) </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">정보 알림 이벤트(300000~399999) </li> 
     </ul> </p> <p>오류와 같은 각 최상위 수준 범위는 재생 오류를 나타내는 101000~101999와 같은 하위 범위로 분할됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">SEEK_ERROR와 같이 사용자가 읽을 수 있는 알림 이벤트에 대한 설명을 포함하는 <span class="codeph"> 문자열입니다</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 메타데이터</span> </td> 
   <td colname="2"> <p>알림에 대한 추가 관련 정보가 들어 있는 키/값 쌍입니다. </p> <p>예를 들어 URL이라는 <span class="codeph"> 키는</span> 오류를 발생시킨 잘못된 URL과 같이 알림과 관련된 URL인 값을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>이 알림에 직접 영향을 준 다른 <span class="codeph"> MediaPlayerNotification</span> 개체에 대한 참조입니다. </p> <p>한 예로, 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림이 있을 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

