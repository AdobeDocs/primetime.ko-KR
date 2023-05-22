---
description: 광고 시그널링 모드는 비디오 스트림이 광고 정보를 받아야 하는 위치를 지정합니다.
title: 광고 신호 모드
exl-id: 1cf81780-ae3b-4bdd-9447-17a2b37bad6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 광고 신호 모드 {#ad-signaling-mode}

광고 시그널링 모드는 비디오 스트림이 광고 정보를 받아야 하는 위치를 지정합니다.

유효한 값은 다음과 같습니다. `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, 및 `PTAdSignalingModeServerMap`.

다음 표에서는 의 효과를 설명합니다. `AdSignalingMode` 다양한 HLS 스트림 유형에 대한 값:

<table frame="all" colsep="1" rowsep="1" id="table_AdSignalingMode"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> </th> 
   <th colname="2" class="entry"><b>기본값</b></th> 
   <th colname="3" class="entry"><b>매니페스트 큐</b></th> 
   <th colname="4" class="entry"><b>광고 서버 맵</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 주문형 비디오(VOD) </td> 
   <td colname="2"> 
    <ul id="ul_E79DA79107364D0D8B46A1859CA75B5C"> 
     <li id="li_B259ED87743F463095071F58DC840E39"> <p>배치 탐지에 서버 맵 사용 </p> </li> 
     <li id="li_8957E4151466467BA6C954E5010E34EA"> <p>광고가 삽입됨 </p> </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_D462C76717D94DE09915BDF6E9B3FB68"> 
     <li id="li_FB46108F4AD9457D99D2618ABEF7DBD1"> <p>배치 탐지에 스트림 내 큐 사용 </p> </li> 
     <li id="li_C3F7FBB98F524CEF97D17318C292E9EA"> <p>프리롤 광고가 메인 스트림에 삽입됩니다. </p> </li> 
     <li id="li_A56E1545F84840DFA6D065DA60E98C31"> <p>주 스트림을 중간 롤 광고로 바꿉니다. </p> </li> 
    </ul> </td> 
   <td colname="4"> 
    <ul id="ul_F10192B1B6F745CBB0D4C1A6D52A57B4"> 
     <li id="li_2ADACF71FA5F4A08A00A3399F5593420"> <p>배치 탐지에 서버 맵 사용 </p> </li> 
     <li id="li_1201085B9C554A4BBD471E7EB2E363AC"> <p>광고가 삽입됨 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 라이브/선형 </td> 
   <td colname="2"> 
    <ul id="ul_82AAC9EE056F49E999F809536A96C2F8"> 
     <li id="li_73BAD2BAA95F4592808B77F8DA436237"> <p>배치 탐지에 매니페스트 큐를 사용합니다. </p> </li> 
     <li id="li_A97B6F61078D4149A984B2412021E103"> <p>광고가 기본 스트림을 대체합니다. </p> </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_CAED2D4F46334D76AE025482881BF843"> 
     <li id="li_A8023845A037482DBFDEF7EF247FECFD"> <p>배치 탐지에 스트림 내 큐 사용 </p> </li> 
     <li id="li_62A3CDAD249344EB89043B2AE0F4D7FF"> <p>광고가 기본 스트림을 대체합니다. </p> </li> 
    </ul> </td> 
   <td colname="4"> 지원되지 않음 </td> 
  </tr> 
 </tbody> 
</table>
