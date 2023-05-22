---
description: TVSDK는 재생을 시작하는 비디오와 같은 미디어 재생 작업이 발생할 때 재생 이벤트를 전달합니다.
title: 재생 이벤트
exl-id: 675dd444-d58c-4316-9d62-b64e6433b650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 재생 이벤트{#playback-events}

TVSDK는 재생을 시작하는 비디오와 같은 미디어 재생 작업이 발생할 때 재생 이벤트를 전달합니다.

모든 재생 관련 이벤트에 대한 알림을 받으려면 의 구현을 등록하십시오. `MediaPlayer.PlaybackEventListener`, 다음 이벤트 콜백을 포함합니다.

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 이벤트 </th> 
   <th colname="2" class="entry"> 의미 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>재생</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> 미디어 소스의 끝에 도달했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> 미디어 소스 재생이 시작되었습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> 선택한 날짜</a> (부동 소수점 비율) </td> 
   <td colname="2"> 사용자 또는 TVSDK가 정속 재생, 되감기 또는 정상 속도로 재생을 재개하는 것과 같은 새로운 재생 속도를 선택했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlay</a> (부동 소수점 비율) </td> 
   <td colname="2"> 새 재생 속도가 화면에 표시됩니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>미디어</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> 미디어 플레이어가 미디어를 준비했습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> 사용 가능한 크기</a> (긴 높이, 긴 폭) </td> 
   <td colname="2"> 미디어 크기를 사용할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>미디어 플레이어</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> state, <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> 알림) </td> 
   <td colname="2"> 미디어 플레이어의 상태가 변경되었습니다. 이 콜백에서 응용 프로그램이 오류를 처리해야 합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChange</a> (긴 프로필, 긴 시간) </td> 
   <td colname="2"> 미디어 플레이어의 현재 프로필이 변경되었습니다. 사용 <span class="codeph"> 프로필</span> 재생 중인 새 프로필을 가져올 속성입니다. 사용 <span class="codeph"> 시간</span> 속성을 사용하여 이 이벤트가 발생한 시간을 가져올 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">다음 경우 중 하나에서 미디어 플레이어가 미디어를 성공적으로 업데이트했습니다. 
    <ul> 
     <li>라이브 자산에 대해 매니페스트를 새로 고치는 경우.</li> 
     <li>VOD 또는 라이브 에셋에 자막이 있고 자막 트랙에 대해 활동이 처음 검색되는 경우. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>매니페스트 및 타임라인</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> ontimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> TimedMeta</a> timedMeta) </td> 
   <td colname="2"> 매니페스트에서 새 시간 메타데이터가 검색되었습니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdate</a> </td> 
   <td colname="2">미디어 플레이어에서 광고를 추가하거나 제거했으므로 업데이트된 타임라인이 있습니다. <p>라이브 자산에 대해 새로 고침된 매니페스트와 이전 광고 브레이크가 타임라인에서 제거되었거나 새 광고 기회(큐 포인트)가 검색되었습니다. 미디어 플레이어는 타임라인에 새 광고를 확인하고 배치하려고 합니다. </p><p> 이 이벤트를 사용하여 타임라인에 업데이트가 있는지(VOD는 재생 중에 변경되지 않음) 확인합니다. 그런 다음 다음을 사용하여 타임라인을 검색할 수 있습니다. <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
