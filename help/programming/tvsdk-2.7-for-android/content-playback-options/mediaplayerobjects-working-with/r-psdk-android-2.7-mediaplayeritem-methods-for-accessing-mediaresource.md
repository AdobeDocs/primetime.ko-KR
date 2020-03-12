---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
uuid: c6e77eb7-cefd-48aa-9373-2b44a96217a5
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 메서드 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>광고 태그</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;String&gt; getAdTags() </span> </td> 
   <td colname="3"> 광고 배치 프로세스에 사용되는 광고 태그 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>라이브 스트림</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive(); </span> </td> 
   <td colname="3"> 스트림이 라이브인 경우 True;VOD인 경우 false입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM 보호</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected(); </span> </td> 
   <td colname="3"> 스트림이 DRM으로 보호되는 경우 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;DRMMetadataInfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> 매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>자막</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions(); </span> </td> 
   <td colname="3"> 자막 트랙을 사용할 수 있으면 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;ClosedCaptionsTrack&gt; getClosedActionsTracks(); </span> </td> 
   <td colname="3"> 사용 가능한 자막 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> SelectClosedCaptionsTrack을 사용하여 선택한 현재 닫힌 캡션 트랙을 <span class="codeph"> 검색합니다 </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> 자막 트랙을 현재 자막 트랙으로 설정합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>대체 오디오 트랙</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio(); </span> </td> 
   <td colname="3"> 스트림에 대체 오디오 트랙이 있으면 true입니다. <p>참고: 기본(기본) 오디오 트랙은 대체 오디오 트랙 목록에도 포함되어 있습니다. </p> <p>Android용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록에 있는 항목 중 하나로 간주합니다. 이로 인해 MediaPlayerItem.hasAlternateAudio가 <span class="codeph"> false를 </span> 반환하는 유일한 경우는 스트림에 오디오가 전혀 없을 때입니다. 컨텐츠에 하나의 오디오 트랙만 있는 경우 이 메서드는 true를 반환하고 <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 는 단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;AudioTrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> [오디오 트랙]을 선택하여 선택한 오디오 트랙을 <span class="codeph"> 검색합니다 </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> 현재 오디오 트랙으로 사용할 오디오 트랙을 선택합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>시간 지정 메타데이터</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata(); </span> </td> 
   <td colname="3"> 스트림에 시간 지정 메타데이터가 연결되어 있으면 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;TimedMetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> 스트림과 연관된 시간 메타데이터 개체의 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>다양한 프로파일(비트 전송률)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic(); </span> </td> 
   <td colname="3"> 스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;Profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> 연결된 비트 전송률 프로파일 목록을 제공합니다. 각 프로필에 대해 해당 비트율, 프로파일의 높이와 너비를 검색할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 프로필 getSelectedProfile() </span> </td> 
   <td colname="3"> 현재 선택한 프로파일을 검색합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>트릭 플레이</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported(); </span> </td> 
   <td colname="3"> 플레이어가 빨리 감기, 되감기 및 다시 시작을 지원하는 경우 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> 트릭 플레이 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부동 getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> 현재 선택한 재생 속도를 검색합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> 이 <span class="codeph"> 항목과 연결된 MediaPlayerItemConfig </span> 인스턴스를 반환합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>미디어 리소스</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> 이 항목과 연결된 미디어 리소스를 반환합니다. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> 이 항목과 연결된 미디어 식별자를 반환합니다. 이 ID는 항목이 MediaPlayerItemLoader.load를 사용하여 로드될 때 <span class="codeph"> 설정됩니다 </span>. </td> 
  </tr> 
 </tbody> 
</table>
