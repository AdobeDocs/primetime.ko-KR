---
description: 미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함으로 영향을 받습니다.
seo-description: 미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함으로 영향을 받습니다.
seo-title: 광고를 사용한 기본 및 사용자 정의 재생 동작
title: 광고를 사용한 기본 및 사용자 정의 재생 동작
uuid: 45e6b0cd-fb0b-4896-b53a-d3bd78a3c1f3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 광고를 사용한 기본 및 사용자 정의 재생 동작{#default-and-customized-playback-behavior-with-ads}

미디어 재생의 동작은 검색, 일시 중지, 빨리 감기 또는 되감기(트릭 재생 모드), 광고 포함으로 영향을 받습니다.

기본 동작을 무시하려면 을 `AdPolicySelector`사용합니다.

>[!IMPORTANT]
>
>TVSDK는 광고 중 검색을 비활성화할 수 있는 방법을 제공하지 않습니다. 광고 중 검색을 비활성화하도록 애플리케이션을 구성하는 것이 좋습니다.

다음 표에서는 TVSDK가 재생 중에 광고 및 광고 브레이크를 처리하는 방법을 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 비디오 활동 </th> 
   <th colname="col2" class="entry"> 기본 TVSDK 동작 정책 </th> 
   <th colname="col3" class="entry">AdPolicySelector를 통해 <span class="codeph"> 사용자 정의 가능</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반적인 재생 중에 광고 중단이 발생합니다. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 라이브/리니어의 경우 광고 나누기가 이미 감시되었더라도 광고 나누기를 재생합니다. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">VOD의 경우 광고 브레이크가 재생되고 광고 브레이크가 시청된 대로 표시됩니다. </li> 
    </ul> </td> 
   <td colname="col3">selectPolicyForAdBreak를 사용하여 광고 나누기에 대해 다른 정책을 <span class="codeph"> 지정합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 분할을 주 컨텐츠로 전달하려고 합니다. </td> 
   <td colname="col2"> 중단된 재생을 완료할 때 건너뛴 마지막 보지 않은 광고 나누기를 재생하고 원하는 검색 위치에서 재생을 다시 시작합니다. </td> 
   <td colname="col3">selectAdBreaksToPlay를 사용하여 재생할 줄바꿈을 <span class="codeph"> 선택합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 분할을 주요 컨텐츠로 역동적으로 검색합니다. </td> 
   <td colname="col2"> 광고 분리를 재생하지 않고 원하는 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">selectAdBreaksToPlay를 사용하여 재생할 줄바꿈을 <span class="codeph"> 선택합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 중단으로 전환됩니다. </td> 
   <td colname="col2"> 검색이 종료된 광고 시작부터 재생합니다. </td> 
   <td colname="col3">selectPolicyForSeekIntoAd를 사용하여 광고 중단과 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 <span class="codeph"> 지정합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 중단으로 뒤쪽으로 이동합니다. </td> 
   <td colname="col2"> 검색이 종료된 광고 시작부터 재생합니다. </td> 
   <td colname="col3">selectPolicyForSeekIntoAd를 사용하여 광고 중단과 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 <span class="codeph"> 지정합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 시청한 광고 분할을 주요 컨텐츠로 앞 또는 뒤로 검색합니다. </td> 
   <td colname="col2"> 건너뛴 마지막 광고 나누기가 이미 감시된 경우 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">selectAdBreaksToPlay를 사용하여 재생할 <span class="codeph"> 줄바꿈</span> 중 하나를 선택하고 TimeLineItem.watched를 사용하여 이미 본 <span class="codeph"> 줄바꿈을 결정합니다</span> . <p>중요: 기본적으로 TVSDK는 광고 중단에 첫 번째 광고를 입력한 후 즉시 시청한 대로 광고 나누기를 표시합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 브레이크에 대해 앞 또는 뒤로 이동하여 감시 광고 브레이크에 들어갑니다. </td> 
   <td colname="col2"> 광고 나누기를 건너뛰고 광고 중단 바로 다음에 있는 위치로 이동합니다. </td> 
   <td colname="col3">광고 중단에 대해 다른 광고 정책(감시 상태가 true로 설정된 경우)을 지정하고 selectPolicyForSeekIntoAd를 사용하여 검색이 끝나는 특정 광고에 <span class="codeph"> 대해 지정합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 응용 프로그램이 트릭-플레이(DVR 모드)에 들어갑니다. 재생 속도는 음수일(되감기) 또는 1보다 클 수 있습니다(빨리 감기). </td> 
   <td colname="col2"> 빨리 감기 또는 되감기 동안 모든 광고를 건너뛰고, 트릭 재생 종료 후 건너뛰었던 마지막 줄바꿈을 재생하고, 중단 재생이 끝나면 사용자가 선택한 트릭 재생 위치로 건너뜁니다. </td> 
   <td colname="col3">selectAdBreaksToPlay를 사용하여 트릭 재생 종료 후 재생할 건너뛰는 부분 <span class="codeph"> 중 하나를 선택합니다</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션에서 사용자 지정 광고 마커를 사용하여 삽입된 광고를 앞으로 검색합니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3">자세한 내용은 <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 현재 재생 위치로 검색 스크럽 막대 표시를 참조하십시오.</a> </td> 
  </tr> 
 </tbody> 
</table>

