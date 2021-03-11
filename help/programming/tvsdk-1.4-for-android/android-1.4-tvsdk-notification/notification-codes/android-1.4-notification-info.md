---
description: 이 표에서는 INFO에 대한 자세한 정보를 제공합니다. 유형 알림을 참조하십시오.
title: INFO 알림 코드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---


# 정보 알림 코드{#info-notification-codes}

이 표에서는 INFO에 대한 자세한 정보를 제공합니다. 유형 알림을 참조하십시오.

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

대부분의 정보 알림에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 코드 </th> 
   <th colname="2" class="entry"> 이름 </th> 
   <th colname="3" class="entry"> 내부 알림 </th> 
   <th colname="4" class="entry"> 메타데이터 키 </th> 
   <th colname="5" class="entry"> 댓글 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>재생</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> 검색 작업이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> 검색 작업이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> CONTENT_</span> <span class="codeph"> IDCURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> 현재 재생 시간이 기본 컨텐츠와 대체 컨텐츠 사이의 테두리를 넘었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE  </span> </td> 
   <td colname="3"> <p>오류 알림. </p> </td> 
   <td colname="4"><span class="codeph"> 주  </span> </td> 
   <td colname="5"> 플레이어 상태가 변경되었습니다. 상태가 ERROR이면 내부 알림은 스위치를 ERROR 상태로 트리거한 오류 알림 객체입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_MARKER  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> 콘텐츠 마커가 수신되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100  </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_</span> <span class="codeph"> URLFRAGMENT_</span> <span class="codeph"> SIZFRAGMENT_DOWNLOAD_</span> <span class="codeph"> DURATIONPERIOD_INDEX</span> </td> 
   <td colname="5"> 비디오 세그먼트 다운로드 방식과 관련된 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101  </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 높이</span> <p><span class="codeph"> 너비</span> </p> </td> 
   <td colname="5"> 비디오 재생 창의 크기가 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>적응형 비트 전송률(ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000  </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 비트 전송률  </span><span class="codeph"> CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> 비디오의 비트 전송률이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 처리</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000  </span> </td> 
   <td colname="2"><span class="codeph"> TIMELINE_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span><span class="codeph"> PERIOD_INDEX  </span> </td> 
   <td colname="5"> 타임라인이 변경되었습니다(예: 대체 컨텐츠가 추가되거나 제거됨). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_PLACEMENT_COMPLETE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> PROPOSED_AD_</span> <span class="codeph"> BREAKACTED_AD_BREAK</span> </td> 
   <td colname="5"> 제안된 광고 브레이크는 <code>primetime-sdk-name</code>에서 수락되고 재생 타임라인에 (전부 또는 일부) 배치됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK  </span> </td> 
   <td colname="5"> 특정 광고 브레이크의 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK  </span> </td> 
   <td colname="5"> 특정 광고 브레이크의 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004  </span> </td> 
   <td colname="2"><span class="codeph"> AD_START  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> </td> 
   <td colname="5"> 특정 광고 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> </td> 
   <td colname="5"> 특정 광고 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006  </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> 진행 상황</span> </td> 
   <td colname="5"> 특정 광고 재생이 해당 특정 광고의 일정 비율에 도달했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007  </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 유형</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> 이름</span> <p><span class="codeph"> 시간</span> </p> </td> 
   <td colname="5"> 매니페스트에서 새 시간 메타데이터가 발견되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008  </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 사용자가 클릭한 광고에 대한 정보를 반환합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_OVERSEED</span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 광고 나누기를 건너뛰었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>늦은 바인딩 오디오(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID  </span><span class="codeph"> CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> 오디오 트랙이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000  </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP  </span> </td> 
   <td colname="5"> 새 DRM 데이터를 사용할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>일반</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일반 정보 이벤트를 표시합니다. 실제로 TVSDK에서 발행되지 않습니다. TVSDK 정보 이벤트에 해당하는 숫자 코드의 끝 부분에 대한 표시자에 불과합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

