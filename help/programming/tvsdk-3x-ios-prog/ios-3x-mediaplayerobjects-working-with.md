---
description: PTMediaPlayer 객체는 미디어 플레이어를 나타냅니다. PTMediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.
title: MediaPlayer 개체 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# MediaPlayer 개체 {#work-with-mediaplayer-objects} 사용

PTMediaPlayer 객체는 미디어 플레이어를 나타냅니다. PTMediaPlayerItem은 플레이어에서 오디오 또는 비디오를 나타냅니다.

## MediaPlayerItem 클래스 {#section_B6F36C0462644F5C932C8AA2F6827071} 정보

미디어 리소스가 성공적으로 로드되면 TVSDK는 해당 리소스에 대한 액세스를 제공하기 위해 `PTMediaPlayerItem` 클래스의 인스턴스를 만듭니다.

`PTMediaPlayer`은 미디어 리소스를 확인하고 연관된 매니페스트 파일을 로드한 다음 매니페스트를 파싱합니다. 리소스 로드 프로세스의 비동기 부분입니다. `PTMediaPlayerItem` 인스턴스는 리소스가 해결된 후 생성되며 이 인스턴스는 미디어 리소스의 해결된 버전입니다. TVSDK는 새로 만든 `PTMediaPlayerItem` 인스턴스에 대한 액세스 권한을 `PTMediaPlayer.currentItem`에 제공합니다.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하려면 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

## MediaPlayer 개체 라이프사이클 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

`PTMediaPlayer` 인스턴스를 만드는 순간부터 종료(재사용 또는 제거)되는 순간까지 이 인스턴스는 한 상태에서 다른 상태로 일련의 전환을 완료합니다.

일부 작업은 플레이어가 특정 상태일 때만 허용됩니다. 예를 들어 `PTMediaPlayerStatusCreated`에서 `play`을(를) 호출할 수 없습니다. 플레이어가 `PTMediaPlayerStatusReady` 상태에 도달한 후에만 이 상태를 호출할 수 있습니다.

상태로 작업하려면

* `PTMediaPlayer.status`으로 MediaPlayer 객체의 현재 상태를 검색할 수 있습니다.
* 상태 목록은 `PTMediaPlayerStatus`에 정의되어 있습니다.

MediaPlayer 인스턴스 라이프사이클에 대한 상태 전환 다이어그램:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

다음 표에서는 추가적인 세부 사항을 제공합니다.

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>발생 시간:</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램에서 <span class="codeph"> playerWithMediaPlayerItem</span>을(를) 호출하여 새 미디어 플레이어를 요청했습니다. 새로 만든 플레이어가 미디어 플레이어 항목을 지정하기를 기다리고 있습니다. 미디어 플레이어의 초기 상태입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램에서 <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>을(를) 호출하고 미디어 플레이어가 로드되고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK에서 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>컨텐츠가 준비되고 광고가 타임라인에 삽입되거나 광고 절차가 실패했습니다. 버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램에서 <span class="codeph"> play</span>을(를) 호출했으므로 TVSDK가 비디오를 재생하려고 합니다. 비디오가 실제로 재생되기 전에 일부 버퍼링이 발생할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램이 미디어를 재생 및 일시 정지하면 미디어 플레이어가 이 상태와 <span class="codeph"> PTMediaPlayerStatusPlaying</span> 사이에서 이동합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달했고 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램에서 미디어 플레이어를 릴리스했습니다. 이 플레이어는 관련된 리소스도 모두 릴리스합니다. 이 인스턴스를 더 이상 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>프로세스 중에 오류가 발생했습니다. 오류가 발생하면 다음에 응용 프로그램을 수행할 수 있는 작업도 영향을 받을 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 프로세스에 대한 피드백을 제공하거나(예: 다음 상태 변경을 기다리는 동안 스피너) 다음 방법을 호출하기 전에 적절한 상태를 기다리는 등의 미디어 재생 단계를 수행할 수 있습니다.