---
description: 이 표에는 INFO 유형 알림에 대한 자세한 정보가 나와 있습니다.
title: 정보 알림 코드
exl-id: 6f813797-b4ef-4e75-a096-d55103b7304b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 4%

---

# 정보 알림 코드{#info-notification-codes}

이 표에는 INFO 유형 알림에 대한 자세한 정보가 나와 있습니다.

## 섹션 제목 {#section_ED4302E363AE48CBA2C3E0B71AE612D8}

대부분의 정보 알림에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 기본 비디오 콘텐츠, 대체 오디오 콘텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함됩니다.

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
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> 없음 </td> 
   <td colname="5"> 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> SEEK_시간</span> </td> 
   <td colname="5"> 찾기 작업이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"><span class="codeph"> SEEK_시간</span> </td> 
   <td colname="5"> 찾기 작업이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <span class="codeph"> CONTENT_ID</span> <span class="codeph"> CURRENT_MEDIA_시간</span> </td> 
   <td colname="5"> 현재 재생 시간이 주 컨텐츠와 대체 컨텐츠 사이의 경계를 넘었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>모든 오류 알림. </p> </td> 
   <td colname="4"><span class="codeph"> 시/도 </span> </td> 
   <td colname="5"> 플레이어 상태가 변경되었습니다. 상태가 ERROR인 경우, 내부 알림은 ERROR 상태로 전환을 트리거한 오류 알림 객체입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_URL</span> <span class="codeph"> FRAGMENT_SIZE</span> <span class="codeph"> FRAGMENT_DOWN_DURATION</span> <span class="codeph"> PERIOD_INDEX</span> </td> 
   <td colname="5"> 비디오 세그먼트가 다운로드되는 방식과 관련된 정보를 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 높이</span> <p><span class="codeph"> 폭</span> </p> </td> 
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
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 비트율 </span><span class="codeph"> CURRENT_MEDIA_시간 </span> </td> 
   <td colname="5"> 비디오의 비트 전송률이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>광고 처리 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> TIMELINE_CHANGE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span><span class="codeph"> PERIOD_INDEX </span> </td> 
   <td colname="5"> 타임라인이 변경되었습니다(예: 대체 컨텐츠가 추가되거나 제거됨). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_ PLACEMENT_COMPLETE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> PROPOSED_AD_BREAK</span> <span class="codeph"> ACCEPTED_AD_BREAK</span> </td> 
   <td colname="5"> 제안된 광고 브레이크가 TVSDK에 의해 수락되어 재생 타임라인에 (전체 또는 일부만) 배치되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 광고 브레이크(_B) </span> </td> 
   <td colname="5"> 특정 광고 브레이크 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> 광고 브레이크(_B) </span> </td> 
   <td colname="5"> 특정 광고 브레이크 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004 </span> </td> 
   <td colname="2"><span class="codeph"> AD_START </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 광고 브레이크(_B)</span> <p><span class="codeph"> 광고</span> </p> </td> 
   <td colname="5"> 특정 광고 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 광고 브레이크(_B)</span> <p><span class="codeph"> 광고</span> </p> </td> 
   <td colname="5"> 특정 광고 재생이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <span class="codeph"> 광고 브레이크(_B)</span> <p><span class="codeph"> 광고</span> </p> <span class="codeph"> 진행 상황</span> </td> 
   <td colname="5"> 특정 광고 재생이 해당 특정 광고의 특정 비율에 도달했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>지연 바인딩 오디오(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID </span><span class="codeph"> CURRENT_MEDIA_시간 </span> </td> 
   <td colname="5"> <p>오디오 트랙이 변경되었습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP </span> </td> 
   <td colname="5"> <p>새 DRM 데이터를 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>일반</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>일반 정보 이벤트를 표시합니다. 실제로 TVSDK에서 발급하지 않았습니다. TVSDK 정보 이벤트에 해당하는 숫자 코드 범위의 끝에 대한 마커입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
