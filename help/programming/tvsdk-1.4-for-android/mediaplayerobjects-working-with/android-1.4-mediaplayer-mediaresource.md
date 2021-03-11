---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
title: MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 메서드 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>광고 태그</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> <p>광고 배치 프로세스에 사용되는 광고 태그 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>라이브 스트림</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> <p>스트림이 라이브이면 true이고,VOD인 경우 false입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM 보호</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected();  </span> </td> 
   <td colname="3"> <p>스트림이 DRM으로 보호되는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> <p>매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>자막</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions();  </span> </td> 
   <td colname="3"> <p>닫힌 캡션 트랙을 사용할 수 있으면 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedActionsTracks();  </span> </td> 
   <td colname="3"> <p>사용 가능한 자막 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> <p><span class="codeph"> SelectClosedCaptionsTrack </span>으로 선택한 현재 닫힌 캡션 트랙을 검색합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack( ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>자막 트랙을 현재 자막 트랙으로 설정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>대체 오디오 트랙</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio();  </span> </td> 
   <td colname="3"> <p>스트림에 대체 오디오 트랙이 있는 경우 true입니다. </p> <p>팁: 기본(기본) 오디오 트랙도 대체 오디오 트랙 목록에 포함되어 있습니다. </p> <p>Android용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록의 항목 중 하나로 간주합니다. 이로 인해 스트림에 오디오가 전혀 없을 때는 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span>이 false를 반환하는 유일한 경우입니다. 내용에 오디오 트랙이 하나만 있으면 이 메서드는 true를 반환하고 <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 는 단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> <p>사용 가능한 대체 오디오 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> <p><span class="codeph"> selectAudioTrack </span>으로 선택한 오디오 트랙을 검색합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack( AudioTrack audioTrack)  </span> </td> 
   <td colname="3"> <p>현재 오디오 트랙으로 사용할 오디오 트랙을 선택합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>시간 지정 메타데이터</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> <p>스트림에 시간 지정 메타데이터가 연결되어 있으면 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> <p>스트림과 연관된 시간 메타데이터 객체의 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> <p>스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> <p>연결된 비트 전송률 프로필 목록을 제공합니다. 각 프로파일에 대해 비트 전송률과 프로필의 높이와 너비를 검색할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>트릭 플레이</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported();  </span> </td> 
   <td colname="3"> <p>플레이어가 빨리 감기, 되감기 및 다시 시작을 지원하는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListgetAvailablePlaybackRate  </span> </td> 
   <td colname="3"> <p>트릭 플레이 기능 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>미디어 리소스</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> <p>이 항목과 연관된 미디어 리소스를 반환합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

