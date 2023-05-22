---
description: 미디어 재생 비헤이비어는 검색, 일시 중지 및 광고 포함에 의해 영향을 받습니다.
title: 광고가 있는 기본 및 사용자 지정된 재생 비헤이비어
exl-id: f4b2f317-c580-45a9-ad79-0cfa6c21848b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 광고가 있는 기본 및 사용자 지정된 재생 비헤이비어 {#default-and-customized-playback-behavior-with-ads}

미디어 재생 비헤이비어는 검색, 일시 중지 및 광고 포함에 의해 영향을 받습니다.

기본 동작을 무시하려면 `PTAdPolicySelector`.

>[!IMPORTANT]
>
>VOD 및 라이브/선형 스트리밍의 경우 타임라인 조정을 수정할 수 없습니다. 즉, 광고가 재생된 후에는 타임라인에서 광고를 제거할 수 없습니다. 사용자가 뒤로 이동하면, 일반적인 정책으로 제거가 되더라도 동일한 광고가 다시 재생됩니다.

>[!IMPORTANT]
>
>TVSDK는 광고 중에 찾기를 비활성화하는 방법을 제공하지 않습니다. Adobe은 광고 중에 찾기를 비활성화하도록 애플리케이션을 구성할 것을 권장합니다.

다음 표에서는 재생 중에 TVSDK에서 광고 및 광고 브레이크를 처리하는 방법을 설명합니다.

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>비디오 활동</b></th> 
   <th colname="col2" class="entry"><b>기본 TVSDK 동작 정책</b></th> 
   <th colname="col3" class="entry"><b>PTAdPolicySelector를 통해 사용할 수 있는 사용자 정의</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 일반 재생 중에 광고 브레이크가 발생합니다. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">건너뛴 브레이크 중 사용할 브레이크 선택 <span class="codeph"> selectAdBreakToPlay</span> 를 사용하여 이미 시청한 브레이크를 확인합니다. <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>중요: 기본적으로 TVSDK는 광고 브레이크에서 첫 번째 광고를 입력한 후 바로 시청한 것으로 광고 브레이크를 표시합니다. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 애플리케이션이 하나 이상의 광고 브레이크를 앞으로 또는 뒤로 이동하여 감시 광고 브레이크로 드롭합니다. </td> 
   <td colname="col2"> 광고 브레이크를 건너뛰고 광고 브레이크 바로 다음 위치로 이동합니다. </td> 
   <td colname="col3">를 사용하여 찾기가 종료된 광고 브레이크(감시 상태가 true로 설정됨) 및 특정 광고에 대해 다른 광고 정책을 지정합니다 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 사용자 지정 광고 마커를 사용하여 삽입된 광고를 애플리케이션에서 찾습니다. </td> 
   <td colname="col2"> 사용자가 선택한 검색 위치로 건너뜁니다. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
