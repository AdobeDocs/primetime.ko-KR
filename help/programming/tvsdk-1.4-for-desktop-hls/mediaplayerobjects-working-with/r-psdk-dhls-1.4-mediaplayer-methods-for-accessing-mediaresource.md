---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 컨텐트 스트림에 대한 정보를 얻을 수 있습니다.
seo-description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 컨텐트 스트림에 대한 정보를 얻을 수 있습니다.
seo-title: MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드
title: MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드
uuid: c2d18f8e-4107-42bc-a975-9b881aadd27b
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 컨텐트 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 메서드 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>라이브 스트림  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isLive():Boolean;  </span> </td> 
   <td colname="3"> <p>스트림이 라이브인 경우 true;VOD인 경우 false입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM 보호</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isProtected():Boolean;  </span> </td> 
   <td colname="3"> <p>스트림이 DRM으로 보호되는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get drmMetadataInfos():벡터.&lt;drmmetadatainfo&gt;;  </span> </td> 
   <td colname="3"> <p>매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>자막</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasClosedCaptions():Boolean;  </span> </td> 
   <td colname="3"> <p>자막 트랙을 사용할 수 있는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get closedCaptionsTracks():Vector.&lt;closedcaptionstrack&gt;;  </span> </td> 
   <td colname="3"> <p>사용 가능한 자막 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get selectedClosedCaptionsTrack():ClosedCaptionsTrack  </span> </td> 
   <td colname="3"> <p><span class="codeph"> SelectClosedCaptionsTrack </span>으로 선택한 현재 닫힌 캡션 트랙을 검색합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(closedCaptionsTrack:com.adobe.mediacore.info:ClosedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>자막 트랙을 현재 자막 트랙으로 설정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>대체 오디오 트랙  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasAlternateAudio():Boolean;  </span> </td> 
   <td colname="3"> <p>스트림에 대체 오디오 트랙이 있는 경우 true입니다. </p> <p>팁: 기본(기본) 오디오 트랙은 대체 오디오 트랙 목록에도 포함되어 있습니다. </p> <p>데스크탑 HLS용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록에 있는 항목 중 하나로 간주합니다. 이로 인해 스트림에 오디오가 전혀 없는 경우에만 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span>이 false를 반환합니다. 컨텐츠에 하나의 오디오 트랙만 있는 경우 이 메서드는 true를 반환하고 <span class="codeph"> get AudioTracks </span>는 단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수는 audioTracks():Vector를 가져옵니다.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수는 audioTracks():Vector를 가져옵니다.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> <p>사용 가능한 대체 오디오 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedAudioTrack():AudioTrack;  </span> </td> 
   <td colname="3"> <p><span class="codeph"> selectAudioTrack </span>으로 선택한 오디오 트랙을 검색합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack:오디오 트랙 )  </span> </td> 
   <td colname="3"> <p>현재 오디오 트랙으로 사용할 오디오 트랙을 선택합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>시간 지정 메타데이터</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasTimedMetadata():Boolean;  </span> </td> 
   <td colname="3"> <p>스트림에 시간 지정 메타데이터가 연결된 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get timedMetadata():Vector.&lt;timedmetadata&gt;;  </span> </td> 
   <td colname="3"> <p>스트림과 연관된 시간 메타데이터 개체의 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isDynamic():Boolean;  </span> </td> 
   <td colname="3"> <p>스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get profiles():Vector.&lt;profile&gt;;  </span> </td> 
   <td colname="3"> <p>연결된 비트 전송률 프로필 목록을 제공합니다. 각 프로필에 대해 해당 비트 전송률과 프로필의 높이와 너비를 검색할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>트릭 플레이  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isTrickPlaySupported():Boolean;  </span> </td> 
   <td colname="3"> <p>플레이어가 빨리 감기, 되감기 및 재시작을 지원하는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get availablePlaybackRates():Vector.&lt;number&gt; </span> </td> 
   <td colname="3"> <p>트릭 플레이 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>미디어 플레이어  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get player():MediaPlayer  </span> </td> 
   <td colname="3"> <p>현재 이 플레이어와 연결된 미디어 플레이어를 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>미디어 리소스</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get resource():MediaResource;  </span> </td> 
   <td colname="3"> <p>이 항목과 연결된 미디어 리소스를 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> function get resourceId():int  </span> </td> 
   <td colname="3"> <p>이 항목과 연결된 미디어 식별자를 반환합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

