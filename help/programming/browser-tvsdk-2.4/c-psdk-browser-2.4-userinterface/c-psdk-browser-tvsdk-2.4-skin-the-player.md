---
description: 다음 정보를 사용하여 플레이어의 스킨을 조정할 수 있습니다. 각 시각적 구문에 대해 해당 비헤이비어가 기본 비헤이비어에 언급됩니다.
title: 선수 껍질 벗기기
exl-id: 4ad50f96-d174-401f-a731-21e5fbfdbe31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# 선수 껍질 벗기기 {#skinning-the-player}

다음 정보를 사용하여 플레이어의 스킨을 조정할 수 있습니다. 각 시각적 구문에 대해 해당 비헤이비어가 기본 비헤이비어에 언급됩니다.

>[!IMPORTANT]
>
>이 문서의 스키닝 세부 정보는 UI 프레임워크에서 생성되는 기본 UI 요소를 위한 것입니다. 플레이어가 이러한 요소를 수정한 경우 스키닝 요소도 변경해야 합니다.

## 컨테이너 div {#section_99B0D598219D4150B57E97D5381B118F}

컨테이너 div의 스타일은 다음과 같습니다.

>[!TIP]
>
>이러한 div는에 나열되어 있습니다. `common-styles.css` 파일.

기본 div의 스타일은 다음과 같습니다.

<table id="table_AC5745DF725543ADBBCD68BA6130DF12"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>기본 Div</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-main-video-div-style</span> </td> 
   <td colname="col2"> <p>비디오가 재생되는 기본 div의 스타일입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .pip-mode-active</span> </td> 
   <td colname="col2"> <p>PIP 모드가 활성 상태일 때 사용됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> videoBehave</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>화면 속 화면(PIP)</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-pip-video-div</span> </td> 
   <td colname="col2"> <p>PIP 비디오가 재생되는 div 스타일입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .view-as-main-video</span> </td> 
   <td colname="col2"> <p>교체되어 기본 비디오로 표시되는 경우 초기 PIP에 적용됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>다중 비디오 보기</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-다중 보기-컨테이너</span> </td> 
   <td colname="col2"> <p>다중 비디오 보기에서 사용됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-다중 보기</span> </td> 
   <td colname="col2"> <p>멀티뷰의 각 비디오에 배치되는 일반적인 css 스타일입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multiview</span> </td> 
   <td colname="col2"> <p>멀티뷰 내의 비디오들 각각을 수용하는 컨테이너가 멀티뷰 상태에 있는 경우. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 다양한 컨트롤 {#section_E9E4A8E3AEBF4BDC89840B84B3B0E737}

다음은 일반 플레이어 컨트롤의 스타일입니다.

>[!TIP]
>
>이러한 스타일은 다음에 나열됩니다. `default-controls.css` 파일.

<table id="table_0ACB6BAB5DAD42DBBD18CA7C0385A261"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control</span> </td> 
   <td colname="col2"> <p>스크러버 및 공간을 제외한 컨트롤 막대의 모든 컨트롤에 적용 가능 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-input-slider</span> </td> 
   <td colname="col2"> <p>입력 슬라이더 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-header</span> </td> 
   <td colname="col2"> <p>패널 머리글 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-vertical-list-menu-item</span> </td> 
   <td colname="col2"> <p>세로 스타일의 메뉴 목록 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-채우기-스페이서</span> </td> 
   <td colname="col2"> <p>컨트롤 막대의 공간 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-hr-분리자</span> </td> 
   <td colname="col2"> <p>가로 규칙 구분 기호 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-title</span> </td> 
   <td colname="col2"> <p>패널 제목 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-close-btn</span> </td> 
   <td colname="col2"> <p>패널을 닫는 단추 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-button-background</span> </td> 
   <td colname="col2"> <p>모든 단추의 배경 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-txt-control</span> </td> 
   <td colname="col2"> <p>텍스트 컨트롤의 기본 스타일입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 컨트롤 막대 {#section_B683B51EC746484B9AA90CB481D637BD}

컨트롤 막대의 스타일은 다음과 같습니다.

<table id="table_681E13F264674F849FAA2523EB65F094"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control-bar</span> (기본 비헤이비어)</td>
   <td colname="col2"> <p>컨트롤 막대에 적용 가능 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 기능 단추 {#section_57FFD242FF674EA2867BCF6CA7F6B855}

>[!NOTE]
>
>다음 표의 문자는 이 그림의 문자와 일치합니다.

스크러빙 바의 스타일은 다음과 같습니다.

<table id="table_2207AD72E72A47FFA03AC748F06A54FD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일(A) </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-스크럽바</span> </td> 
   <td colname="col2"> <p>컨트롤 막대의 스크러빙 막대 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-buffer-progress-bar</span> </td> 
   <td colname="col2"> <p>스크러빙 막대의 버퍼 진행률 표시줄 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-seek-to-bar</span> </td> 
   <td colname="col2"> <p>사용자가 스크러빙 바를 찾을 때 스크러빙 바의 상태 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-playback-progress-bar</span> </td> 
   <td colname="col2"> <p>일반 재생 중 스크러빙 막대 상태 </p> </td> 
  </tr>
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-progress-bar-play-head</span> </td>
   <td colname="col2"> <p>재생하는 동안 스크러빙 바에서 헤드 재생 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-ad-marker-bar</span> </td>
   <td colname="col2"> <p>광고 표식 막대 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrush-bar .ptp-ad-marker</span> </td>
   <td colname="col2"> <p>광고 마커 </p> </td>
  </tr>
 </tbody>
</table>

기본 동작은 다음과 같습니다.

* `scrubBarBehavior`
* `bufferProgressBarBehavior`
* `playHeadBehavior`
* `playProgressBarBehavior`
* `seekToBarBehavior`

## 재생/일시 중지 단추 {#section_F1F40A948D0049C5A4D8EA5F2A475CAA}

재생/일시 중지 버튼의 스타일은 다음과 같습니다.

<table id="table_975C2293222A4782A8C75A6149C1AD27">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(B) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause</span> </td>
   <td colname="col2"> <p>컨트롤 막대에서 재생 일시 중지 단추. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td>
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> 일시 정지 상태에서 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td> 
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> 재생 상태 </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `playPauseButtonBehavior`.

## 볼륨 {#section_23E17BD2343948F8A2CEE1C8BEE2F874}

볼륨 버튼을 구성하는 스타일은 다음과 같습니다.

<table id="table_8F9831F36A4D427CA31C9FFA4173170D">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(C) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><span class="codeph"> .ptp-volume-control</span>
     <ul id="ul_B12ADDFB83EA40FD8B4E92AF418AA4B4">
      <li id="li_7DA8143A69ED4E7D8A560B9FF75D6BA7"><span class="codeph"> .expanded</span> </li>
      <li id="li_D8CCAD45D81C4850B6903FE261833AE6"><span class="codeph"> .vertical</span> </li>
     </ul> </p> </td>
   <td colname="col2"> <p>컨트롤 막대의 볼륨 컨트롤
     <ul id="ul_2C60F018FDCB458885738AC378C02F61">
      <li id="li_6B19572B504A4BBF9C97DC29C0E92A1D">컨트롤이 확장된 양식인 경우 </li>
      <li id="li_6489E422E1944D5194CBDFC8383D2F30">컨트롤이 세로 형식인 경우 </li>
     </ul> </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume</span> </td>
   <td colname="col2"> <p>컨트롤 막대의 볼륨 단추 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.min-volume-state</span> </td>
   <td colname="col2"> <p>볼륨이 최소 상태일 때 </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.mute-state</span> </td>
   <td colname="col2"> <p>볼륨이 음소거 상태일 때 </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 다음과 같습니다 `volumeBehavior` 및 `muteButtonBehavior`.

볼륨 슬라이더의 스타일은 다음과 같습니다.

<table id="table_E3DC93F8FC614C30AADAE259D18F10EF">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(D) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-slider</span> </td>
   <td colname="col2"> <p>볼륨 슬라이더입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-hidden</span> </td>
   <td colname="col2"> <p>볼륨 슬라이더가 숨겨진 상태입니다. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `volumeSliderBehavior`.

## 되감기 {#section_06EE608FC54A4CF5B5DF9DC743CFC740}

다음은 되감기 단추의 스타일입니다.

<table id="table_0ACB116582D54B188E9F5B5C03D3A615">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(E) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>컨트롤 막대의 되감기 단추입니다. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `rewindButtonBehavior`.

## 시간 {#section_0E6549B3DF6D4C10947D445A5F8EEA7F}

컨트롤 막대에 남은 시간을 표시하는 스타일은 다음과 같습니다.

<table id="table_CEE62BFF5FB04FDCBBE1331E0D727EBA">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(F) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-txt-display-time</span> </td>
   <td colname="col2"> <p>컨트롤 막대에 남은 시간 표시 </p> </td>
  </tr>
</tbody>
</table>

기본 비헤이비어는 입니다. `timeRemainingBehavior`.

## 빠른 되감기 {#section_F6E6C65BD3BD493A89915DF9B92933BA}

다음은 빠른 되감기 단추의 스타일입니다.

<table id="table_25BB4966B709402383AB6A6822FC1999">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(G) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>컨트롤 막대의 빠른 되감기 단추입니다. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `fastRewindButtonBehavior`.

## 느리게 되감기 {#section_38A22BB8681B430F8C6808C3BD21FB4E}

다음은 느린 되감기 단추의 스타일입니다.

<table id="table_E623C374622A497C91E22333D77AF8F6">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(H) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slowrewind</span> </td>
   <td colname="col2"> <p>컨트롤 막대에서 느리게 되감기 단추입니다. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `slowRewindButtonBehavior`.

## 앞으로 느림 {#section_92ACF092EECC4A5EAF6AA090C05E552E}

다음은 앞으로 감기 단추의 스타일입니다.

<table id="table_88C1CF5DB2D84EDBA01AC62B70509B08">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(I) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slowforward</span> </td>
   <td colname="col2"> <p>컨트롤 막대에서 앞으로 감기 단추입니다. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `slowForwardButtonBehavior`.

## 앞으로 감기 {#section_F90ED8B3739B49ACAB1F12DF18F0E4D6}

다음은 앞으로 감기 버튼의 스타일입니다.

<table id="table_F166BD1E8B934B34AF3690BBBAD894B7">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일(J) </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastforward</span> </td>
   <td colname="col2"> <p>컨트롤 막대의 앞으로 이동 단추. </p> </td>
  </tr>
 </tbody>
</table>

기본 비헤이비어는 입니다. `fastForwardButtonBehavior`.

## 오디오 트랙 {#section_1CDF4FA5A1C14DB6B9C96579FFA1057C}

오디오 트랙을 구성하는 스타일은 다음과 같습니다.

<table id="table_22FC521D786B45EB84F230894FFECE79">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>오디오 추적 단추(K)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-audio-track</span> </td>
   <td colname="col2"> <p>컨트롤 막대의 오디오 추적 단추입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> audioTrackButtonBevior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>오디오 트랙 선택 패널(L)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-panel</span> </td> 
   <td colname="col2"> <p>오디오 트랙을 선택하는 패널입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> audioTrackSelectionPanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>오디오 트랙 선택 헤더(M)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>에 대한 헤더 <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>오디오 트랙 선택 메뉴(N)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-menu</span> </td>
   <td colname="col2"> <p>의 메뉴 항목 <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
 </tbody>
</table>

## 공유 {#section_B2ADC76E76304A68AD648A00A12B676E}

공유를 구성하는 스타일은 다음과 같습니다.

<table id="table_3264C472809D462B8FC16680B96B1AC9">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일 </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>소셜 미디어 공유 단추(O)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video</span> </td> 
   <td colname="col2"> <p>컨트롤 막대에서 열릴 소셜 미디어 공유 단추 <span class="codeph"> ptp-share-video-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> shareVideoButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>공유 비디오 패널(P)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel</span> </td>
   <td colname="col2"> <p>소셜 공유 옵션을 표시하는 패널입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> shareVideoPanelBehave</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>비디오 메뉴 공유(Q)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>에 대한 헤더 <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .share-video-panel-menu</span> </td>
   <td colname="col2"> <p>의 메뉴 <span class="codeph"> ptp-share-video-panel</span> 소셜 미디어에서 콘텐츠를 공유하는 모든 옵션을 표시합니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel-menu-item</span> </td>
   <td colname="col2"> <p>의 메뉴 항목 <span class="codeph"> share-video-panel-menu</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-facebook</span> </td>
   <td colname="col2"> <p>facebook에서 콘텐츠를 공유할 수 있는 메뉴 항목입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-twitter</span> </td>
   <td colname="col2"> <p>twitter 시 콘텐츠를 공유할 수 있는 메뉴 항목입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-google-plus</span> </td>
   <td colname="col2"> <p>Google Plus에서 콘텐츠를 공유할 수 있는 메뉴 항목입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-linkedin</span> </td>
   <td colname="col2"> <p>linkedIn에서 콘텐츠를 공유할 수 있는 메뉴 항목입니다. </p> </td>
  </tr>
 </tbody>
</table>

## 폐쇄 캡션 {#section_A01BA68218564DA0B7D6BF51F045D7AB}

폐쇄 캡션을 구성하는 스타일은 다음과 같습니다.

<table id="table_777C7034C9424F8C841DABD480FFAC47">
 <thead>
  <tr>
   <th colname="col1" class="entry"> 스타일 </th>
   <th colname="col2" class="entry"> 설명 </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>폐쇄 캡션 단추(R)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-closed-caption</span> </td>
   <td colname="col2"> <p>다음 <span class="uicontrol"> 폐쇄 캡션</span> 단추를 클릭합니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> closedCaptionButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .on-state</span> </td>
   <td colname="col2"> <p>비디오에 대해 캡션이 활성화되었습니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>폐쇄 캡션 패널(S)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-panel</span> </td>
   <td colname="col2"> <p>폐쇄 캡션용 패널입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> closedCaptionLanguagePanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>폐쇄 캡션 언어(T)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-panel:</span> </td>
   <td colname="col2"> <p>에 대한 헤더 <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-menu: </span> </td>
   <td colname="col2"> <p>닫힘 캡션 패널의 메뉴. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>폐쇄 캡션 옵션(U)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-btn</span> </td>
   <td colname="col2"> <p>다음 <span class="uicontrol"> 옵션</span> [폐쇄 캡션 옵션] 패널의 단추입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-panel</span> </td>
   <td colname="col2"> <p>선택 캡션 패널의 옵션 패널입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-menu-item</span> </td>
   <td colname="col2"> <p>닫힘 캡션 패널의 메뉴 항목입니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .selected</span> </td>
   <td colname="col2"> <p>를 선택합니다. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-done-btn</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 완료</span> [폐쇄 캡션 옵션] 패널의 헤더에 있는 단추입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-menu</span> </td> 
   <td colname="col2"> <p>선택 캡션의 옵션 메뉴 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-main-menu</span> </td> 
   <td colname="col2"> <p>선택 캡션 옵션의 기본 메뉴입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-sub-menu</span> </td> 
   <td colname="col2"> <p>선택 캡션 옵션의 하위 메뉴입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-opacity-slider</span> </td> 
   <td colname="col2"> <p>닫힌 캡션 옵션의 불투명도 슬라이더입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-separator</span> </td> 
   <td colname="col2"> <p>선택 캡션 옵션 구분 기호입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-item</span> </td> 
   <td colname="col2"> <p>선택 캡션 <span class="uicontrol"> 옵션</span> 메뉴 항목. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-preview-panel</span> </td> 
   <td colname="col2"> <p>선택 캡션 미리 보기 패널. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-footer</span> </td> 
   <td colname="col2"> <p>선택 캡션 옵션 바닥글입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-reset-button</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 재설정</span> [닫힌 캡션 옵션] 패널의 바닥글에 있는 단추입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-apply-button</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 적용</span> [닫힌 캡션 옵션] 패널의 바닥글에 있는 단추입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> closedCaptionOptionsPanelBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## 추가 옵션(V) {#section_18E25CF8A8964FFD9026A8A833089CE3}

추가 옵션을 구성하는 스타일은 다음과 같습니다.
<table id="table_EC6EF88E2EDE4B8EBB1C14F87A6161FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 추가 옵션</span> 단추를 클릭합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options.ptp-control-bar-btn</span> </td> 
   <td colname="col2"> <p>다음 <span class="codeph"> ptp-btn-more-options</span> 컨트롤 막대에서 사용됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel</span> </td> 
   <td colname="col2"> <p>추가 옵션 제어판 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu</span> </td> 
   <td colname="col2"> <p>기타 옵션 제어판 메뉴. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu-item</span> </td> 
   <td colname="col2"> <p>기타 옵션 제어판 메뉴 항목. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 비헤이비어는 입니다. `moreOptionsButtonBehavior`.

## PIP 단추(W) {#section_1EE039DEA99541D391B30BD1DF72A83E}

다음 스타일은 [!UICONTROL PIP<] 단추:

<table id="table_EE2E882C87E24D39B8D5347686F29E55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-pip</span> </td> 
   <td colname="col2"> <p>컨트롤 막대의 PIP 단추. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> pipButtonBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## 전체 화면(X) {#section_158A19DFB30E4432A67E4A74A7CBA563}

전체 화면을 구성하는 스타일은 다음과 같습니다.

<table id="table_5941835F31AC4E9CBA9702AB8D813B8F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-fullscreen</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 전체 화면</span> 단추를 클릭합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 비헤이비어는 입니다. `fullScreenButtonBehavior`.

## 트릭 플레이(Y) {#section_AE6F83BB7EE2497FB13CD94A8316192D}

다음은 트릭 플레이를 구성하는 스타일입니다.

<table id="table_F1ADAC0A4B4E48669828690BDEB4BC09"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-control-bar-trick-play-rate</span> </td> 
   <td colname="col2"> <p>컨트롤 막대의 트릭 속도 표시 구성 요소입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 비헤이비어는 입니다. `trickPlayRateDisplayBehavior`.

## 멀티뷰(Z) {#section_58EFAE7263BA45D3A4E2AB7309A9CAA7}

멀티뷰를 구성하는 스타일은 다음과 같습니다.

<table id="table_84B37D7410EE40DFA7A8BB8431C6DCF0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-multiview</span> </td> 
   <td colname="col2"> <p>다음 <span class="uicontrol"> 다중 보기</span> 컨트롤 막대의 단추 및 초기 상태 <span class="uicontrol"> 멀티뷰</span> 단추를 클릭합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">기본 비헤이비어는 입니다. <span class="codeph"> multiViewButtonBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
 </tbody> 
</table>

## 축소판 {#section_0AFD932975634BB08387EEE7D3BFC438}

축소판을 구성하는 스타일은 다음과 같습니다.

<table id="table_968136A8BBA042A7A8E79739B8F92F55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-progress-bar-thumb-nail</span> </td> 
   <td colname="col2"> <p>썸네일의 진행률 표시줄입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 비헤이비어는 입니다. `thumbnailPreviewBehavior`.

## 오류 메시지 {#section_AC9858EE1B5A4FF4947E383C663B6AB5}

오류 메시지를 구성하는 스타일은 다음과 같습니다.

<table id="table_7F4C156170DB4AFFA7DEE06F00449506"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel</span> </td> 
   <td colname="col2"> <p>플레이어의 오류 메시지를 표시하는 패널입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-icon</span> </td> 
   <td colname="col2"> <p>오류 메시지가 있을 때 패널에 표시되는 아이콘입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-message</span> </td> 
   <td colname="col2"> <p>표시되는 오류 메시지입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 비헤이비어는 입니다. `errorMessagePanelBehavior`.

## 버퍼링 오버레이 {#section_2FE8FDE2599E42BAA7411D0D38FA0A88}

축소판을 구성하는 스타일은 다음과 같습니다.

<table id="table_1FECE1DC29B8434B886751A29455F004"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-버퍼링-오버레이</span> </td> 
   <td colname="col2"> <p>버퍼링 오버레이 컨트롤입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

기본 오버레이는 입니다. `bufferingOverlayBehavior`.

## 특정 선택기 {#section_51F735AEF82E41E890FF59E031A0DB89}

다음은 앞으로 감기 버튼의 스타일입니다.

<table id="table_E77EDC7D227348E79C7E73FB5D46F992"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 스타일 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ad-break</span> </td> 
   <td colname="col2"> <p>광고가 재생되는 동안 컨트롤 패널의 상태입니다. </p> <p>다음 항목에 적용됩니다. 
     <ul id="ul_D5076303DCD94D968682289823D1A9F2"> 
      <li id="li_4290C4B2D48546E3AD023BED6CAAE395"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_72A3D3E916E44A55BA170407EAB0527D"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_A0BAEBB0E01B402EB83E3CE9B92B15CC"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_FDF2CEDB0A854098907FF9CBCF1A61C1"><span class="codeph"> .ptp-btn-slowforward</span> </li> 
      <li id="li_CD2E14DB3DD64C10A253DA23FBE04A04"><span class="codeph"> .ptp-btn-slowforward</span> </li> 
      <li id="li_A230359E8F7F4571A9EBFF0E4C2462D7"><span class="codeph"> .ptp-btn-slowrewind</span> </li> 
      <li id="li_5711A315872F4FA59FDDF0EF0AFD03C6"><span class="codeph"> .ptp-btn-more-options </span> </li> 
      <li id="li_71C8E76077A84ED590160AB5ABFCC0D7"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_4A3113C0360F4F708AAA96AB316FA057"><span class="codeph"> .ptp-btn-closed-caption </span> </li> 
      <li id="li_901A0186D65A48A1B774DC555CEC5367"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
      <li id="li_2331583C01C2482B8EE72979FBF111DB"><span class="codeph"> .ptp-btn-pip </span> </li> 
      <li id="li_7BB39BDF5E294AEB8FA3DCD9F9A29468"><span class="codeph"> .ptp-btn-rewind</span> </li> 
      <li id="li_E4FEF5A7486A40F6A5FE1119BD63AFEF"><span class="codeph"> .ptp-scrush-bar</span> </li> 
      <li id="li_12153547558A4871842EE0416BCCA8B2"><span class="codeph"> .ptp-seek-to-bar</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multi-view</span> </td> 
   <td colname="col2"> <p>멀티뷰 상태에 있는 컨트롤의 상태입니다. </p> <p>다음 항목에 적용됩니다. 
     <ul id="ul_A8AC653C30814AC49041F3B58A2106F4"> 
      <li id="li_0407167DA21647A8A6960DFE55A33F42"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_EA71CAF41CDC41DE859A85CE482BE97C"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_F3A998C51A034C22A914EAEFF19FFEA7"><span class="codeph"> .ptp-btn-closed-caption</span> </li> 
      <li id="li_022F871ABC894C9BA879B3AF3D341202"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .fullscreen-state</span> </td> 
   <td colname="col2"> <p>플레이어가 전체 화면 모드에 있습니다. </p> <p>다음 항목에 적용됩니다. 
     <ul id="ul_B235C1D339F64B2FAC6BC72F03807616"> 
      <li id="li_6E050EE74C604FDAB4C9C0447F547A9D"><span class="codeph"> .ptp-control-bar </span> </li> 
      <li id="li_67D54B1A41764B2DA544479CDA1C901C"><span class="codeph"> .ptp-btn-fullscreen</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
