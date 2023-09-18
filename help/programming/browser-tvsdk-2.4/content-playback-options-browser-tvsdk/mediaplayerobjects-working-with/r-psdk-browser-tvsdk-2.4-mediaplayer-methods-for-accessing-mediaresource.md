---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.
title: MediaResource 정보에 액세스하기 위한 MediaPlayer 속성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# MediaResource 정보에 액세스하기 위한 MediaPlayer 속성{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 목적 </th> 
   <th colname="2" class="entry"> 속성 </th> 
   <th colname="3" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 라이브 스트림 </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> 스트림이 라이브이면 True이고, VOD이면 False입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 폐쇄 캡션 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> 자막 트랙을 사용할 수 있는 경우 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> 사용 가능한 자막 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> 다음 옵션을 사용하여 선택한 자막트랙을 검색합니다. <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 대체 오디오 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>스트림에 대체 오디오 트랙이 있는 경우 True입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selected오디오 트랙 </span> </td> 
   <td colname="3"> 
    <pre>
      현재 선택된 오디오 트랙과 함께 선택된 오디오 트랙을 검색합니다. 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 시간 메타데이터 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMeta </span> </td> 
   <td colname="3"> 스트림에 시간 메타데이터가 연결된 경우 True입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMeta </span> </td> 
   <td colname="3"> 스트림과 연결된 시간이 지정된 메타데이터 개체의 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 여러 프로필(비트 전송률) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 프로필 </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 이 스트림과 연결된 관련 비트 전송률 프로필 목록을 제공합니다. <p>참고: 각 프로필에 대한 비트 전송률과 프로필의 높이 및 너비를 검색할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 미디어 리소스 </td> 
   <td colname="2"> <span class="codeph"> 리소스 </span> </td> 
   <td colname="3"> 이 항목과 연결된 미디어 리소스를 반환합니다. </td> 
  </tr> 
 </tbody> 
</table>
