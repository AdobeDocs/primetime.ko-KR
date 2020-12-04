---
description: 이 표에서는 INFO 유형 알림에 대한 자세한 정보를 제공합니다.
seo-description: 이 표에서는 INFO 유형 알림에 대한 자세한 정보를 제공합니다.
seo-title: INFO 알림 코드
title: INFO 알림 코드
uuid: 10145ce6-9eb0-4829-85dd-1acfe97b07e8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---


# INFO 알림 코드{#info-notification-codes}

이 표에서는 INFO 유형 알림에 대한 자세한 정보를 제공합니다.

대부분의 정보 알림에는 관련 메타데이터가 포함되어 있습니다. 예를 들어 다운로드하지 못한 리소스의 URL입니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

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
   <td colname="1"><span class="codeph"> 30000  </span> </td> 
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
   <td colname="4"> <p> 없음 </p> </td> 
   <td colname="5"> 검색 작업이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE  </span> </td> 
   <td colname="3"> 없음 </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> 검색 작업이 완료되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> 플레이어 상태가 변경되었습니다. state가 ERROR이면 내부 알림이 ERROR 상태로 전환을 트리거한 오류 알림 오브젝트입니다. </td> 
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
   <td colname="4"><span class="codeph"> 비트 전송률  </span> </td> 
   <td colname="5"> 비디오 비트 전송률이 변경되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>늦은 바인딩 오디오(LBA)</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>오디오 트랙이 변경되었습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>자막</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000  </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLE_TRACK_CHANGE  </span> </td> 
   <td colname="3"> <p>없음 </p> </td> 
   <td colname="4"> <p>없음 </p> </td> 
   <td colname="5"> <p>자막 트랙이 변경되었습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

