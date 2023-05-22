---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.
title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
exl-id: 5e4434ce-d2b1-4b7b-b3d1-77f62ff46d36
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 방법 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>태그 추가</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> 광고 배치 프로세스에 사용되는 광고 태그 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>라이브 스트림</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 isLive(); </span> </td> 
   <td colname="3"> 스트림이 라이브이면 True이고, VOD이면 False입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM 보호</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 isProtected(); </span> </td> 
   <td colname="3"> 스트림이 DRM으로 보호되면 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;drmmetadatainfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> 매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>폐쇄 캡션</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 hasClosedCaptions(); </span> </td> 
   <td colname="3"> 자막 트랙을 사용할 수 있는 경우 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;closedcaptionstrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> 사용 가능한 자막 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> 선택한 현재 닫힌 캡션 트랙을 검색합니다. <span class="codeph"> 선택ClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> 자막 트랙을 현재 자막 트랙으로 설정합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>대체 오디오 트랙</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 hasAlternateAudio(); </span> </td> 
   <td colname="3"> 스트림에 대체 오디오 트랙이 있는 경우 True입니다. <p>참고: 기본(기본) 오디오 트랙도 대체 오디오 트랙 목록의 일부입니다. </p> <p>Android용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록의 항목 중 하나로 간주합니다. 이 때문에, <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 스트림에 오디오가 전혀 없는 경우 false를 반환합니다. 컨텐츠에 하나의 오디오 트랙만 있는 경우 이 메서드는 true를 반환하고, <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> 선택한 오디오 트랙을 검색합니다. <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> 오디오 트랙을 현재 오디오 트랙으로 선택합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>시간 메타데이터</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 hasTimedMetadata(); </span> </td> 
   <td colname="3"> 스트림에 시간 메타데이터가 연결된 경우 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> 스트림과 연결된 시간이 지정된 메타데이터 개체의 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>여러 프로필(비트 전송률)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 isDynamic(); </span> </td> 
   <td colname="3"> 스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 목록&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> 연결된 비트 전송률 프로필 목록을 제공합니다. 각 프로필에 대해 비트 전송률과 프로필의 높이 및 너비를 검색할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 프로필 getSelectedProfile() </span> </td> 
   <td colname="3"> 현재 선택한 프로필을 검색합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>트릭 플레이</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 부울 isTrickPlaySupported(); </span> </td> 
   <td colname="3"> 플레이어가 빨리 감기, 되감기 및 재개를 지원하는 경우 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> 트릭 재생 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> getSelectedPlaybackRate() 부동 </span> </td> 
   <td colname="3"> 현재 선택한 재생 속도를 검색합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> 다음을 반환합니다. <span class="codeph"> 미디어 플레이어 항목 구성 </span> 이 항목과 연결된 인스턴스. </td> 
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
   <td colname="3"> 이 항목과 연결된 미디어 식별자를 반환합니다. 이 ID는 항목을 사용하여 로드할 때 설정됩니다. <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
