---
description: 미디어 재생 비헤이비어는 찾기, 일시 정지, 빨리 감기 또는 되감기(트릭 재생 모드) 및 광고 포함에 의해 영향을 받습니다.
title: 광고가 있는 기본 및 사용자 지정된 재생 비헤이비어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 광고가 있는 기본 및 사용자 지정된 재생 비헤이비어{#default-and-customized-playback-behavior-with-ads}

미디어 재생 비헤이비어는 찾기, 일시 정지, 빨리 감기 또는 되감기(트릭 재생 모드) 및 광고 포함에 의해 영향을 받습니다.

기본 동작을 무시하려면 `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>브라우저 TVSDK는 광고 중에 찾기를 비활성화하는 방법을 제공하지 않습니다. Adobe은 광고 중에 찾기를 비활성화하도록 애플리케이션을 구성할 것을 권장합니다.

다음 표에서는 브라우저 TVSDK가 재생 중에 광고 및 광고 브레이크를 처리하는 방법을 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 비디오 활동 </th> 
   <th colname="col2" class="entry"> 기본 브라우저 TVSDK 동작 정책 </th> 
   <th colname="col3" class="entry">다음을 통해 사용 가능한 사용자 지정 <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반 재생 중에 광고 브레이크가 발생합니다. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 라이브/선형의 경우, 광고 브레이크를 이미 시청한 경우에도 재생합니다. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">VOD의 경우 는 광고 브레이크를 재생하고 시청한 광고 브레이크를 표시합니다. </li> 
    </ul> </td> 
   <td colname="col3">을 사용하여 광고 브레이크에 대한 다른 정책을 지정합니다. <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 브레이크를 넘어 기본 컨텐츠로 이동합니다. </td> 
   <td colname="col2"> 건너뛴 마지막 관찰되지 않은 광고 브레이크를 재생하고 브레이크 재생이 완료되면 원하는 찾기 위치에서 재생을 재개합니다. </td> 
   <td colname="col3">을(를) 사용하여 재생할 생략된 브레이크 선택 <span class="codeph"> selectAdBreakToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 브레이크를 뒤로 하여 기본 컨텐츠로 이동합니다. </td> 
   <td colname="col2"> 광고 브레이크를 재생하지 않고 원하는 찾기 위치로 건너뜁니다. </td> 
   <td colname="col3">을(를) 사용하여 재생할 생략된 브레이크 선택 <span class="codeph"> selectAdBreakToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 브레이크를 찾습니다. </td> 
   <td colname="col2"> 찾기가 종료된 광고 시작부터 재생됩니다. </td> 
   <td colname="col3">를 사용하여 찾기가 종료된 특정 광고 및 광고 브레이크에 대해 다른 광고 정책을 지정합니다 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 브레이크를 거꾸로 찾습니다. </td> 
   <td colname="col2"> 찾기가 종료된 광고 시작부터 재생됩니다. </td> 
   <td colname="col3">를 사용하여 찾기가 종료된 특정 광고 및 광고 브레이크에 대해 다른 광고 정책을 지정합니다 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 시청한 광고 브레이크를 앞뒤로 이동하여 기본 콘텐츠를 검색합니다. </td> 
   <td colname="col2"> 건너뛴 마지막 광고 브레이크가 이미 시청된 경우 가 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">건너뛴 브레이크 중 사용할 브레이크 선택 <span class="codeph"> selectAdBreakToPlay</span> 를 사용하여 이미 시청한 브레이크를 확인합니다. <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 브레이크를 앞으로 또는 뒤로 이동하여 감시 광고 브레이크로 드롭합니다. </td> 
   <td colname="col2"> 광고 브레이크를 건너뛰고 광고 브레이크 바로 다음 위치로 이동합니다. </td> 
   <td colname="col3">를 사용하여 찾기가 종료된 광고 브레이크(감시 상태가 true로 설정됨) 및 특정 광고에 대해 다른 광고 정책을 지정합니다 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 사용자 지정 광고 마커를 사용하여 삽입된 광고를 애플리케이션에서 찾습니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">자세한 내용은 <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 검색 창 사용 시 검색 처리</a> </td> 
  </tr> 
 </tbody> 
</table>

## 사용자 지정 광고 비헤이비어 설정 {#section_custom_ad_behaviors}

의 광고 콘텐츠 팩토리에서 기본 동작을 설정할 수 있습니다. `retrieveAdPolicySelectorCallbackFunc` 메서드를 사용합니다. 다음을 사용할 수 있습니다. `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd`, 및 `selectAdBreaksToPlay` 컨텐츠 팩토리에서 정책을 선택하는 메서드입니다.
