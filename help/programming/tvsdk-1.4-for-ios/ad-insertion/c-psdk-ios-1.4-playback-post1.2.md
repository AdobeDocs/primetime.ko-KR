---
description: 미디어 재생의 동작은 검색, 일시 중지 및 광고 포함에 영향을 받습니다.
seo-description: 미디어 재생의 동작은 검색, 일시 중지 및 광고 포함에 영향을 받습니다.
seo-title: 광고를 사용한 기본 및 사용자 정의 재생 동작
title: 광고를 사용한 기본 및 사용자 정의 재생 동작
uuid: cc996e5c-bee2-451b-96cb-088df1694188
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 광고{#default-and-customized-playback-behavior-with-ads}을(를) 사용하는 기본 및 사용자 지정된 재생 동작

미디어 재생의 동작은 검색, 일시 중지 및 광고 포함에 영향을 받습니다.

기본 동작을 무시하려면 `PTAdPolicySelector`을 사용하십시오.

>[!IMPORTANT]
>
>VOD 및 실시간/선형 스트리밍의 경우 타임라인 조정을 수정할 수 없습니다. 즉, 재생 후에는 타임라인에서 광고를 제거할 수 없습니다. 사용자가 다시 찾아오면 일반 정책이 제거되었더라도 동일한 광고가 다시 재생됩니다.

>[!IMPORTANT]
>
>TVSDK는 광고 중 검색을 비활성화할 수 있는 방법을 제공하지 않습니다. Adobe은 광고 중 검색을 비활성화하도록 애플리케이션을 구성하는 것이 좋습니다.

다음 표에서는 TVSDK가 재생되는 동안 광고 및 광고 할인을 처리하는 방법에 대해 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 비디오 활동 </th> 
   <th colname="col2" class="entry"> 기본 TVSDK 동작 정책 </th> 
   <th colname="col3" class="entry"><span class="codeph"> PTAdPolicySelector</span>를 통해 사용자 지정 가능 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반 재생 중에 광고 중단이 발생합니다. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>를 사용하여 재생할 생략된 휴식 시간 중 하나를 선택하고 <span class="codeph"> PTAdBreak.isViewed</span>을 사용하여 이미 본 휴식 시간을 결정합니다. <p> <p>중요: 기본적으로 TVSDK는 광고 중단에 첫 번째 광고를 입력한 후 즉시 시청되는 광고 중단으로 표시됩니다. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 중단에 대해 앞 또는 뒤로 이동하여 감시 광고 중단으로 들어갑니다. </td> 
   <td colname="col2"> 광고 중단을 건너뛰고 광고 중단 바로 다음 위치로 이동합니다. </td> 
   <td colname="col3">광고 중단에 대해 다른 광고 정책(감시 상태가 true로 설정된 경우)을 지정하고 <span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 검색이 끝나는 특정 광고에 대해 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 사용자 지정 광고 마커를 사용하여 삽입된 광고를 앞으로 검색합니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

