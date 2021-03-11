---
description: TVSDK는 광고가 포함된 컨텐츠의 재생 동작을 사용자 정의하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.
title: 광고 재생을 위한 API 요소
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 광고 재생을 위한 API 요소 {#api-elements-for-ad-playback}

TVSDK는 광고가 포함된 컨텐츠의 재생 동작을 사용자 정의하는 데 사용할 수 있는 클래스와 메서드를 제공합니다.

다음 API 요소는 재생을 사용자 정의하는 데 유용합니다.

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>API 요소  </b></th> 
   <th colname="col2" class="entry"> <b>광고를 지원하는 컨텐츠</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> 광고 메타데이터  </span> </td> 
   <td colname="col2">광고 나누기를 뷰어에서 시청한 것으로 표시할지를, 그리고 예인 경우 표시할 시기를 제어합니다. <span class="codeph"> setAdBreakAsViewed</span> 및 <span class="codeph"> getAdBreakAsViewed</span>을 사용하여 감시 정책을 설정하고 가져옵니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 광고 중단에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> 광고에 대해 가능한 재생 정책을 열거합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector  </span> </td> 
   <td colname="col2"> TVSDK 광고 비헤이비어를 사용자 정의할 수 있는 인터페이스입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> 기본 TVSDK 비헤이비어를 구현하는 클래스입니다. 응용 프로그램은 전체 인터페이스를 구현하지 않고 기본 동작을 사용자 지정하기 위해 이 클래스를 재정의할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>가져온 광고 분리를 제외한 재생 현지 시간입니다. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal을 참조하십시오</span>. <p>여기에서 검색은 스트림의 로컬 시간을 기준으로 수행됩니다. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>타임라인의 가상 위치가 로컬 위치로 변환됩니다. </p> </li> 
    </ul> <p>중요: <span class="codeph"> MediaPlayer</span>의 <span class="codeph"> getLocalTime</span>은 동적 스플라인 광고 없이 원본 컨텐트에 상대적인 현재 시간을 반환합니다. <span class="codeph"> get</span> LocalTime  <span class="codeph"> </span> AdBreakdown은 원래 컨텐트에 상대적인 휴식 시간 시작 시간을 반환합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatchedproperty</span> 입니다. 뷰어가 광고를 시청했는지 여부를 나타냅니다. </td> 
  </tr> 
 </tbody> 
</table>