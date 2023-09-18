---
description: TVSDK는 광고가 포함된 콘텐츠의 재생 동작을 사용자 지정하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.
title: 광고 재생용 API 요소
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 광고 재생용 API 요소 {#api-elements-for-ad-playback}

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
   <td colname="col1"><span class="apiname"> AdvertisingMeta </span> </td> 
   <td colname="col2">광고 브레이크를 시청자가 시청한 것으로 표시해야 하는지 여부와 표시해야 하는 시점을 제어합니다. 다음을 사용하여 감시 정책 설정 및 가져오기 <span class="codeph"> setAdBreakAsWatched</span> 및 <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 광고 브레이크에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> 광고에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> TVSDK 광고 동작의 맞춤화를 허용하는 인터페이스. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 기본 TVSDK 동작을 구현하는 클래스입니다. 응용 프로그램에서 이 클래스를 재정의하여 전체 인터페이스를 구현하지 않고도 기본 동작을 사용자 지정할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>이는 배치된 광고 브레이크를 제외한 재생의 로컬 시간입니다. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekTolocal</span>. <p>여기에서, 찾기는 스트림 내의 로컬 시간에 관하여 발생한다. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>타임라인에서 가상 위치가 로컬 위치로 변환됩니다. </p> </li> 
    </ul> <p>중요 사항:  <span class="codeph"> getLocalTime</span> 위치: <span class="codeph"> MediaPlayer</span> 동적으로 스플라이싱된 광고 없이 원래 콘텐츠에 상대적인 현재 시간을 반환합니다. <span class="codeph"> getLocalTime</span> 위치: <span class="codeph"> AdBreak</span> 원래 컨텐츠를 기준으로 브레이크의 시작 시간을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> 속성. 뷰어가 광고를 시청했는지 여부를 나타냅니다. </td> 
  </tr> 
 </tbody> 
</table>
