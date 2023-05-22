---
description: TVSDK는 광고가 포함된 콘텐츠의 재생 동작을 사용자 지정하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.
title: 광고 재생용 API 요소
exl-id: 459995c2-1d6f-4414-94a6-2c0b24098c14
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 광고 재생용 API 요소{#api-elements-for-ad-playback}

TVSDK는 광고가 포함된 콘텐츠의 재생 동작을 사용자 지정하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.

다음 API 요소는 재생을 사용자 지정하는 데 유용합니다.

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API 요소 </th> 
   <th colname="col2" class="entry"> 광고를 지원하는 콘텐츠 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMeta</span> </td> 
   <td colname="col2">광고 브레이크를 시청자가 시청한 것으로 표시해야 하는지 여부와 표시해야 하는 시점을 제어합니다. 다음을 사용하여 감시 정책 설정 및 가져오기 
    <pre>
     다음 
     <span class="codeph"> adBreakAsWatched</span> 속성.
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 광고 브레이크에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> 광고에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> TVSDK 광고 동작의 맞춤화를 허용하는 인터페이스. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> 기본 TVSDK 동작을 구현하는 클래스입니다. 응용 프로그램에서 이 클래스를 재정의하여 전체 인터페이스를 구현하지 않고도 기본 동작을 사용자 지정할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>이는 배치된 광고 브레이크를 제외한 재생의 로컬 시간입니다. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekTolocal</span>. <p>여기서, 찾기는 스트림 내의 로컬 시간에 관하여 발생한다. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>타임라인에서 가상 위치가 로컬 위치로 변환됩니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> 감시됨</span>. <p>뷰어가 광고를 시청했는지 여부를 나타냅니다. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>원래 콘텐츠에 상대적인 광고 브레이크 또는 광고의 시작 위치 및 기간입니다. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>배치된 모든 광고 브레이크를 고려한 후 가상 타임라인에서 광고 브레이크 또는 광고의 시작 위치 및 기간입니다. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
