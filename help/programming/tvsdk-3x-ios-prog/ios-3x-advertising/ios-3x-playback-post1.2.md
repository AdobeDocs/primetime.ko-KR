---
description: 미디어 재생의 동작은 검색, 일시 중지 및 광고 포함에 의해 영향을 받습니다.
title: 광고를 사용한 기본 및 사용자 정의된 재생 동작
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# 광고 {#default-and-customized-playback-behavior-with-ads}이(가) 있는 기본 및 사용자 지정된 재생 동작

미디어 재생의 동작은 검색, 일시 중지 및 광고 포함에 의해 영향을 받습니다.

기본 동작을 무시하려면 `PTAdPolicySelector`을(를) 사용합니다.

>[!IMPORTANT]
>
>VOD 및 실시간/선형 스트리밍의 경우 타임라인 조정을 수정할 수 없습니다. 즉, 광고를 재생한 후에는 타임라인에서 제거할 수 없습니다. 사용자가 다시 찾아오면 일반 정책이 제거되었더라도 동일한 광고가 다시 재생됩니다.

>[!IMPORTANT]
>
>TVSDK는 광고 중 검색을 비활성화할 수 있는 방법을 제공하지 않습니다. Adobe은 광고 중 검색을 비활성화하도록 애플리케이션을 구성하는 것이 좋습니다.

다음 표에서는 TVSDK가 재생 중에 광고 및 광고 할인을 처리하는 방법을 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>비디오 활동</b></th> 
   <th colname="col2" class="entry"><b>기본 TVSDK 비헤이비어 정책</b></th> 
   <th colname="col3" class="entry"><b>PTAdPolicySelector를 통해 사용자 정의 가능</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반적인 재생 중에 광고 중단이 발생합니다. </td> 
   <td colname="col2"></td> 
   <td colname="col3"><span class="codeph"> selectPolicyForAdBreak</span>을 사용하여 광고 중단에 대해 다른 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 내역을 주 컨텐츠로 전달하려고 합니다. </td> 
   <td colname="col2"> 일시 중단된 재생을 완료한 후 원하는 검색 위치에서 재생을 다시 시작하여 건너뛴 마지막으로 보지 않은 광고 나누기를 재생합니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>을 사용하여 재생할 줄바꿈을 건너뛴 항목을 선택합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 나누기를 주 컨텐츠로 뒤로 이동합니다. </td> 
   <td colname="col2"> 광고 분리를 재생하지 않고 원하는 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>을 사용하여 재생할 줄바꿈을 건너뛴 항목을 선택합니다.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 차단을 검색합니다. </td> 
   <td colname="col2"> 검색이 끝난 광고의 처음부터 재생됩니다. </td> 
   <td colname="col3"><span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 광고 중단과 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 광고 중단으로 뒤돌아옵니다. </td> 
   <td colname="col2"> 검색이 끝난 광고의 처음부터 재생됩니다. </td> 
   <td colname="col3"><span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 광고 중단과 검색이 끝나는 특정 광고에 대해 다른 광고 정책을 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 시청한 광고 나누기를 주 컨텐츠로 앞 또는 뒤로 검색합니다. </td> 
   <td colname="col2"> 건너뛴 마지막 광고 나누기가 이미 지켜진 경우 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"><span class="codeph"> selectAdBreaksToPlay</span>을 사용하여 재생할 건너뛰는 줄바꿈 중 하나를 선택하고 <span class="codeph"> PTAdBreak.isViewed</span>을 사용하여 이미 본 나누기를 결정합니다. <p> <p>중요: 기본적으로 TV SDK는 광고 노출에 첫 번째 광고를 입력한 후 즉시 시청되는 광고를 표시합니다. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 분리를 앞뒤로 이동하거나 뒤로 이동하여 감시 광고 브레이크로 드롭할 수 있습니다. </td> 
   <td colname="col2"> 광고 브레이크를 건너뛰고 광고 브레이크 바로 다음에 있는 위치로 이동합니다. </td> 
   <td colname="col3">광고 나누기에 대해 다른 광고 정책(감시 상태가 true로 설정된 상태로)을 지정하고 <span class="codeph"> selectPolicyForSeekIntoAd</span>을 사용하여 검색이 끝나는 특정 광고에 대해 지정합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 사용자 지정 광고 마커를 사용하여 삽입된 광고를 검색합니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>