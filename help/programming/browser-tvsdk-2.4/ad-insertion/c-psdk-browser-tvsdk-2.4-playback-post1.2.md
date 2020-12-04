---
description: 미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함에 영향을 받습니다.
seo-description: 미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함에 영향을 받습니다.
seo-title: 광고를 사용한 기본 및 사용자 정의 재생 동작
title: 광고를 사용한 기본 및 사용자 정의 재생 동작
uuid: 58f11167-a764-4647-8490-05ca66eb6c47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# 광고{#default-and-customized-playback-behavior-with-ads}을(를) 사용하는 기본 및 사용자 지정된 재생 동작

미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함에 영향을 받습니다.

기본 동작을 무시하려면 `AdBreakPolicySelector`을 사용하십시오.

>[!IMPORTANT]
>
>브라우저 TVSDK는 광고 중 검색을 비활성화할 수 있는 방법을 제공하지 않습니다. Adobe은 광고 중 검색을 비활성화하도록 애플리케이션을 구성하는 것이 좋습니다.

다음 표에서는 Browser TVSDK가 재생되는 동안 광고 및 광고 할인을 처리하는 방법에 대해 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 비디오 활동 </th> 
   <th colname="col2" class="entry"> 기본 브라우저 TVSDK 동작 정책 </th> 
   <th colname="col3" class="entry"><span class="codeph"> AdBreakPolicySelector </span>를 통해 사용자 지정 가능 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반 재생 중에 광고 중단이 발생합니다. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 라이브/리니어의 경우 광고 나누기가 이미 감시되었더라도 광고 나누기를 재생합니다. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">VOD의 경우, 광고 휴식 시간을 재생하고 보는 대로 광고 중단을 표시한다. </li> 
    </ul> </td> 
   <td colname="col3"><span class="codeph"> selectPolicyForAdBreak</span>을 사용하여 광고 중단에 대한 다른 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 분할을 주요 컨텐츠로 전달합니다. </td> 
   <td colname="col2"> 일시 중단된 재생을 완료할 때 건너뛴 마지막으로 보지 않은 광고 중단과 원하는 검색 위치에서 재생을 다시 시작합니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>를 사용하여 재생할 줄바꿈을 선택합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 차단을 지나 기본 컨텐츠로 뒤돌아옵니다. </td> 
   <td colname="col2"> 광고 분리를 재생하지 않고 원하는 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>를 사용하여 재생할 줄바꿈을 선택합니다.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 중단으로 전환됩니다. </td> 
   <td colname="col2"> 검색 결과가 끝난 광고의 처음부터 재생됩니다. </td> 
   <td colname="col3">광고 중단과 <span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 중단으로 뒤돌아옵니다. </td> 
   <td colname="col2"> 검색 결과가 끝난 광고의 처음부터 재생됩니다. </td> 
   <td colname="col3">광고 중단과 <span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 시청한 광고 나누기를 주 컨텐츠로 앞 또는 뒤로 이동합니다. </td> 
   <td colname="col2"> 건너뛴 마지막 광고 나누기가 이미 표시된 경우 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>를 사용하여 재생할 생략된 휴식 시간 중 하나를 선택하고 <span class="codeph"> isViewed</span>을 사용하여 이미 본 휴식 시간을 결정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 중단에 대해 앞 또는 뒤로 이동하여 감시 광고 중단으로 들어갑니다. </td> 
   <td colname="col2"> 광고 중단을 건너뛰고 광고 중단 바로 다음 위치로 이동합니다. </td> 
   <td colname="col3">광고 중단에 대해 다른 광고 정책(감시 상태가 true로 설정된 경우)을 지정하고 <span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 검색이 끝나는 특정 광고에 대해 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 사용자 지정 광고 마커를 사용하여 삽입된 광고를 앞으로 검색합니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">자세한 내용은 검색 막대를 사용할 때 <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 검색 처리</a>을 참조하십시오. </td> 
  </tr> 
 </tbody> 
</table>

## 사용자 지정 광고 비헤이비어 설정 {#section_custom_ad_behaviors}

`retrieveAdPolicySelectorCallbackFunc` 메서드에서 광고 콘텐츠 팩터리에서 기본 동작을 설정할 수 있습니다. 콘텐츠 팩터리에서 `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd` 및 `selectAdBreaksToPlay` 메서드를 사용하여 정책을 선택할 수 있습니다.
