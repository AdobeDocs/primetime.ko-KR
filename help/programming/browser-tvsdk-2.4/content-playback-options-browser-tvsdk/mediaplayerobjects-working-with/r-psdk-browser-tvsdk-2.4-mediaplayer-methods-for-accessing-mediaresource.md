---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-title: MediaResource 정보에 액세스하기 위한 MediaPlayer 속성
title: MediaResource 정보에 액세스하기 위한 MediaPlayer 속성
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# MediaResource 정보에 액세스하기 위한 MediaPlayer 특성{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.

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
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> 스트림이 라이브인 경우 true;VOD인 경우 false입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 자막 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> 자막 트랙을 사용할 수 있는 경우 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> 사용 가능한 자막 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> <span class="codeph"> selectClosedCaptionsTrack </span>으로 선택한 닫힌 캡션 트랙을 검색합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 대체 오디오 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>스트림에 대체 오디오 트랙이 있는 경우 true입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> 사용 가능한 대체 오디오 트랙 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack  </span> </td> 
   <td colname="3"> 
    <pre>
      현재 선택한 오디오 트랙을 
     <span class="codeph"> selectAudioTrack </span> 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 시간 지정 메타데이터 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata  </span> </td> 
   <td colname="3"> 스트림에 시간 지정 메타데이터가 연결된 경우 true입니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata  </span> </td> 
   <td colname="3"> 스트림과 연관된 시간 메타데이터 개체 목록을 제공합니다. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 여러 프로필(비트 속도) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 프로필  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 이 스트림과 연결된 비트 전송률 프로필 목록을 제공합니다. <p>참고: 각 프로파일의 비트 전송률과 프로파일의 높이와 너비를 검색할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 미디어 리소스 </td> 
   <td colname="2"> <span class="codeph"> 리소스  </span> </td> 
   <td colname="3"> 이 항목과 연결된 미디어 리소스를 반환합니다. </td> 
  </tr> 
 </tbody> 
</table>

