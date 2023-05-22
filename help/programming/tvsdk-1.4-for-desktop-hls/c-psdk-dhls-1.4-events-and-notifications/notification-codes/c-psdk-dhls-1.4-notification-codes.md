---
description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
title: 알림 코드
exl-id: 7ea079f1-658d-45ab-891d-044b7b4ff4ec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 개요 {#notification-codes-overview}

TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 개체는 플레이어의 상태와 관련된 정보를 제공합니다. TVSDK는 시간순으로 정렬된 알림 개체 목록을 제공하며 각 알림에는 다음 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 요소 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 유형 </td> 
   <td colname="2"> 알림 유형. 이 속성은 플랫폼에 따라 INFO, WARN 또는 ERROR 값이 가능한 열거 형식을 참조합니다. 알림의 최상위 그룹입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 코드 </td> 
   <td colname="2">알림에 지정된 숫자 표시: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">오류 알림 이벤트(100000~199999) </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">경고 알림 이벤트(200000~299999) </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">300000부터 399999까지 정보 알림 이벤트 </li> 
    </ul> <p>오류와 같은 각 최상위 범위는 재생 오류를 나타내는 101000~101999과 같은 하위 범위로 구분됩니다. </p>
    <pre>
     열거형 
     <span class="codeph"> mediacore.PSDKErrorCode</span> 가능한 값을 나열합니다.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 이름 </td> 
   <td colname="2">사람이 인식할 수 있는 코드 설명(예: <span class="codeph"> 찾기 오류</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 메타데이터 </td> 
   <td colname="2">알림에 대한 추가 관련 정보가 포함된 키/값 쌍입니다. 예를 들어 <span class="codeph"> URL</span> 은 오류를 일으킨 잘못된 URL과 같이, 알림과 관련된 URL인 값과 쌍을 이루게 됩니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">다른 참조에 대한 참조 <span class="codeph"> MediaPlayerNotification</span> 이 알림에 직접 영향을 미친 개체입니다. 한 가지 예는 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림일 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </td> 
  </tr> 
 </tbody> 
</table>
