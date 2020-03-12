---
description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-description: TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.
seo-title: 알림 코드
title: 알림 코드
uuid: a7b77a5c-9873-45cf-8499-aa00270a7ad6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 개요 {#notification-codes-overview}

TVSDK 알림 시스템은 진단 메타데이터를 제공하는 다양한 오류, 경고 및 정보 알림을 생성합니다.

알림 개체는 플레이어의 상태와 관련된 정보를 제공합니다. TVSDK는 시간순으로 정렬된 알림 객체 목록을 제공하며 각 알림에는 다음 메타데이터가 포함됩니다.

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 요소 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> 알림 유형입니다. 플랫폼에 따라 이 속성은 INFO, WARN 또는 ERROR 값이 가능한 열거형 유형을 참조합니다. 알림을 위한 최상위 수준의 그룹화입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> code </td> 
   <td colname="2">알림에 할당된 숫자 표현: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">오류 알림 이벤트(100000~19999) </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">경고 알림 이벤트(20000~29999) </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">정보 알림 이벤트(300000~399999) </li> 
    </ul> <p>오류와 같은 각 최상위 수준 범위는 재생 오류를 나타내는 101000~101999와 같은 하위 범위로 분할됩니다. </p>
    <ph>
     열거 <span class="codeph"> mediacore.PSDKErrorCode는</span> 가능한 값을 나열합니다.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">SEEK_ERROR와 같이, 사람이 읽을 수 있는 코드 설명이 들어 있는 <span class="codeph"> 문자열</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 메타데이터 </td> 
   <td colname="2">알림에 대한 추가 관련 정보가 들어 있는 키/값 쌍입니다. 예를 들어 URL이라는 <span class="codeph"> 키는</span> 오류를 발생시킨 잘못된 URL과 같이 알림과 관련된 URL인 값과 쌍을 이루게 됩니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">이 알림에 직접 영향을 준 다른 <span class="codeph"> MediaPlayerNotification</span> 개체에 대한 참조입니다. 한 예로, 타임라인 삽입 충돌에 직접 해당하는 광고 삽입 실패에 대한 알림이 있을 수 있습니다. 일부 알림은 내부 알림을 제공하지 않습니다. </td> 
  </tr> 
 </tbody> 
</table>

