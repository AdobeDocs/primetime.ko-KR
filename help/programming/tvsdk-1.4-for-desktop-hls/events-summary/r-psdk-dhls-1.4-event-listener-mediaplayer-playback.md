---
description: 애플리케이션은 TVSDK에서 발송하는 이벤트를 수신하여 플레이어에서 활동 및 플레이어의 변화하는 상태를 모니터링할 수 있습니다.
title: 재생 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 재생 이벤트 {#playback-events}

애플리케이션은 TVSDK에서 발송하는 이벤트를 수신하여 플레이어에서 활동 및 플레이어의 변화하는 상태를 모니터링할 수 있습니다.

TVSDK는 재생을 시작하는 비디오와 같은 미디어 재생 작업이 발생할 때 재생 이벤트를 전달합니다. 모든 재생 관련 이벤트에 대한 알림을 받으려면 수신자를 `MediaPlayer` 개체.

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이벤트 </th> 
   <th colname="2" class="entry"> 의미 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>재생</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> 선택된 비율(_S)</a> </td> 
   <td colname="2"> 사용자 또는 TVSDK가 정속 재생, 되감기 또는 정상 속도로 재생을 재개하는 것과 같은 새로운 재생 속도를 선택했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 새 재생 속도가 화면에 표시됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_변경됨</a> </td> 
   <td colname="2"> 미디어의 현재 플레이헤드 위치가 변경되었습니다. 현재 시간이 변경될 때 250ms 이상마다 주기적으로 발송됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>미디어 플레이어</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> 상태 변경됨</a> </td> 
   <td colname="2"> 미디어 플레이어의 상태가 변경되었습니다. 이 이벤트의 콜백에서 응용 프로그램이 오류를 처리해야 합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> 프로필 변경됨</a> </td> 
   <td colname="2">미디어 플레이어의 현재 프로필이 변경되었습니다. 사용 <span class="codeph"> ProfileEvent.profile</span> 재생 중인 새 프로필을 가져올 속성입니다. 사용 <span class="codeph"> 시간</span> 속성을 사용하여 이 이벤트가 발생한 시간을 가져올 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem 이벤트입니다.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_생성됨</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> 이(가) 만들어졌습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem 이벤트입니다.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> 항목 업데이트됨</a> </td> 
   <td colname="2">다음 경우 중 하나에서 미디어 플레이어가 미디어를 성공적으로 업데이트했습니다. 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">라이브 자산에 대해 매니페스트를 새로 고치는 경우. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">VOD 또는 라이브 에셋에 자막이 있고 자막 트랙에 대해 활동이 처음 검색되는 경우. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>캡션 및 오디오</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem 이벤트입니다.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> 캡션 업데이트됨</a> </td> 
   <td colname="2">미디어 스트림 및 <span class="codeph"> closedCaptionsTracks</span> 컬렉션이 업데이트되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>매니페스트 및 타임라인</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> 타임라인 업데이트됨</a> </td> 
   <td colname="2">미디어 플레이어에서 광고를 추가하거나 제거했으므로 업데이트된 타임라인이 있습니다. <p>라이브 자산에 대해 새로 고침된 매니페스트와 이전 광고 브레이크가 타임라인에서 제거되었거나 새 광고 기회(큐 포인트)가 검색되었습니다. 미디어 플레이어는 타임라인에 새 광고를 확인하고 배치하려고 합니다. </p> <p> 이 이벤트를 사용하여 타임라인에 업데이트가 있는지(VOD는 재생 중에 변경되지 않음) 확인합니다. 그런 다음 다음을 사용하여 타임라인을 검색할 수 있습니다. <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
