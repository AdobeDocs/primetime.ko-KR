---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.
title: MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# MediaResource 정보에 액세스하기 위한 MediaPlayer 메서드{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 방법 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>라이브 스트림 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>스트림이 라이브이면 True이고, VOD이면 False입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM 보호</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>스트림이 DRM으로 보호되면 True입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get drmMetadataInfos(): Vector.&lt;drmmetadatainfo&gt;; </span> </td> 
   <td colname="3"> <p>매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>폐쇄 캡션</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get hasClosedCaptions():부울; </span> </td> 
   <td colname="3"> <p>자막 트랙을 사용할 수 있는 경우 True입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get closedCaptionsTracks():Vector.&lt;closedcaptionstrack&gt;; </span> </td> 
   <td colname="3"> <p>사용 가능한 자막 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get selectedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>선택한 현재 닫힌 캡션 트랙을 검색합니다. <span class="codeph"> 선택ClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(closedCaptionsTrack: com.adobe.mediacore.info:ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>자막 트랙을 현재 자막 트랙으로 설정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>대체 오디오 트랙 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>스트림에 대체 오디오 트랙이 있는 경우 True입니다. </p> <p>팁: 기본(기본) 오디오 트랙도 대체 오디오 트랙 목록의 일부입니다. </p> <p>Desktop HLS용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록의 항목 중 하나로 간주합니다. 이 때문에, <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 스트림에 오디오가 전혀 없는 경우 false를 반환합니다. 컨텐츠에 하나의 오디오 트랙만 있는 경우 이 메서드는 true를 반환하고, <span class="codeph"> 오디오 트랙 가져오기 </span> 단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get audioTracks():Vector.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get audioTracks():Vector.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> <p>사용 가능한 대체 오디오 트랙 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get selectedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>선택한 오디오 트랙을 검색합니다. <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack ) </span> </td> 
   <td colname="3"> <p>오디오 트랙을 현재 오디오 트랙으로 선택합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>시간 메타데이터</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get hasTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>스트림에 시간 메타데이터가 연결된 경우 True입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get timedMetadata():Vector.&lt;timedmetadata&gt;; </span> </td> 
   <td colname="3"> <p>스트림과 연결된 시간이 지정된 메타데이터 개체의 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get profiles():Vector.&lt;profile&gt;; </span> </td> 
   <td colname="3"> <p>연결된 비트 전송률 프로필 목록을 제공합니다. 각 프로필에 대해 비트 전송률과 프로필의 높이 및 너비를 검색할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>트릭 플레이 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get isTrickPlaySupported():부울; </span> </td> 
   <td colname="3"> <p>플레이어가 빨리 감기, 되감기 및 재개를 지원하는 경우 True입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get availablePlaybackRates():Vector.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>트릭 재생 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>미디어 플레이어 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>현재 이 플레이어와 연결된 미디어 플레이어를 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>미디어 리소스</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 함수 get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>이 항목과 연결된 미디어 리소스를 반환합니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 함수 get resourceId():int </span> </td> 
   <td colname="3"> <p>이 항목과 연결된 미디어 식별자를 반환합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
