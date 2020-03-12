---
description: 애플리케이션은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변경 상태를 모니터링할 수 있습니다.
seo-description: 애플리케이션은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변경 상태를 모니터링할 수 있습니다.
seo-title: 재생 이벤트
title: 재생 이벤트
uuid: 6d6491d7-cf25-4130-8388-68b8c028bb71
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 재생 이벤트 {#playback-events}

애플리케이션은 TVSDK에서 전달하는 이벤트를 수신하여 플레이어의 활동과 플레이어의 변경 상태를 모니터링할 수 있습니다.

TVSDK는 재생을 시작하는 비디오와 같은 미디어 재생 작업이 발생할 때 재생 이벤트를 전달합니다. 모든 재생 관련 이벤트에 대한 알림을 받으려면 다음 이벤트에 대한 `MediaPlayer` 개체에 리스너를 등록합니다.

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
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> 사용자 또는 TVSDK는 빠른 앞으로, 되감기 또는 정상적인 속도로 재생을 다시 시작하는 등의 새로운 재생 속도를 선택했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 새로운 재생 속도가 화면에 표시됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 미디어의 현재 재생 헤드 위치가 변경되었습니다. 250ms 이상마다 현재 시간이 변경되면 주기적으로 전달됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>미디어 플레이어</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> 미디어 플레이어의 상태가 변경되었습니다. 응용 프로그램은 이 이벤트의 콜백에서 오류를 처리해야 합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">미디어 플레이어의 현재 프로필이 변경되었습니다. ProfileEvent <span class="codeph"> .profile</span> 속성을 사용하여 재생되는 새 프로필을 가져옵니다. 이 이벤트가 발생한 시간을 가져오려면 <span class="codeph"> time</span> 속성을 사용합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem 이벤트를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">MediaPlayerItem <span class="codeph"> 이</span> 만들어졌습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem 이벤트를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">다음 중 한 가지 경우에 미디어 플레이어가 미디어를 업데이트했습니다. 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">라이브 자산에 대해 매니페스트 새로 고침이 발생하는 경우 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">VOD 또는 라이브 에셋에 자막이 있는 경우 자막 트랙에 대한 활동이 처음 검색됩니다. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>캡션 및 오디오</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem 이벤트를 참조하십시오.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">미디어 스트림에서 새로운 자막 트랙이 검색되었고 <span class="codeph"> 자막트랙</span> 컬렉션이 업데이트되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>매니페스트 및 타임라인</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">미디어 플레이어에서 광고를 추가하거나 제거했으므로 업데이트된 타임라인이 있습니다. <p>라이브 자산에 대해 새로 고쳐진 매니페스트와 이전 광고 브레이크가 타임라인에서 제거되었거나 새로운 광고 기회(큐 포인트)가 발견되었습니다. 미디어 플레이어는 타임라인에 새로운 광고를 확인하고 배치합니다. </p> <p> 이 이벤트를 사용하여 타임라인에 업데이트가 있는지 확인하십시오(재생 중에 VOD가 변경되지 않음). 그런 다음 MediaPlayer.timeline을 사용하여 타임라인을 검색할 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> 수</a>있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

