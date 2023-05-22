---
description: PTMediaPlayer 객체는 미디어 플레이어를 나타냅니다. PTMediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.
title: MediaPlayer 개체 작업
exl-id: 57dd455e-e78c-4e5b-80af-070ae7982864
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# MediaPlayer 개체 작업 {#work-with-mediaplayer-objects}

PTMediaPlayer 객체는 미디어 플레이어를 나타냅니다. PTMediaPlayerItem은 플레이어의 오디오 또는 비디오를 나타냅니다.

## MediaPlayerItem 클래스 정보 {#section_B6F36C0462644F5C932C8AA2F6827071}

미디어 리소스가 성공적으로 로드되면 TVSDK는 `PTMediaPlayerItem` 클래스에 대한 액세스 권한을 제공합니다.

다음 `PTMediaPlayer` 미디어 리소스를 확인하고, 연결된 매니페스트 파일을 로드하고, 매니페스트를 구문 분석합니다. 리소스 로드 프로세스의 비동기적 부분입니다. 다음 `PTMediaPlayerItem` 리소스가 해결된 후 인스턴스가 생성되며, 이 인스턴스는 미디어 리소스의 해결된 버전입니다. TVSDK는 새로 만든 항목에 대한 액세스 권한을 제공합니다 `PTMediaPlayerItem` 인스턴스 - `PTMediaPlayer.currentItem`.

>[!TIP]
>
>미디어 플레이어 항목에 액세스하기 전에 리소스가 성공적으로 로드될 때까지 기다려야 합니다.

## MediaPlayer 개체 수명 주기 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

만든 순간부터 `PTMediaPlayer` 인스턴스를 종료(재사용 또는 제거)하는 순간까지 이 인스턴스는 한 상태에서 다른 상태로 일련의 전환을 완료합니다.

일부 작업은 플레이어가 특정 상태에 있을 때만 허용됩니다. 예: 호출 `play` 위치: `PTMediaPlayerStatusCreated` 은(는) 허용되지 않습니다. 플레이어가 다음에 도달한 후에만 이 상태를 호출할 수 있습니다. `PTMediaPlayerStatusReady` 상태.

상태로 작업하려면

* 를 사용하여 MediaPlayer 개체의 현재 상태를 검색할 수 있습니다. `PTMediaPlayer.status`.
* 상태 목록은에 정의되어 있습니다. `PTMediaPlayerStatus`.

MediaPlayer 인스턴스의 라이프사이클에 대한 상태 전환 다이어그램:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

다음 표에는 추가 세부 정보가 나와 있습니다.

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>다음과 같은 경우 발생</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>응용 프로그램에서 를 호출하여 새 미디어 플레이어를 요청했습니다. <span class="codeph"> playerWithMediaPlayerItem</span>. 새로 만든 플레이어가 미디어 플레이어 항목 지정을 기다리고 있습니다. 미디어 플레이어의 초기 상태입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>애플리케이션이 호출함 <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>, 미디어 플레이어를 로드하는 중입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK가 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>콘텐츠가 준비되었고 광고가 타임라인에 삽입되었거나 광고 절차가 실패했습니다. 버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>애플리케이션이 을(를) 호출했습니다. <span class="codeph"> play</span>따라서 TVSDK에서 비디오를 재생하려고 합니다. 일부 버퍼링은 비디오가 실제로 재생되기 전에 발생할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>애플리케이션이 미디어를 재생하고 일시 중지하면 미디어 플레이어가 이 상태와 간에 이동합니다. <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달하여 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>애플리케이션이 미디어 플레이어를 릴리스했습니다. 또한 연결된 리소스를 릴리스합니다. 이 인스턴스를 더 이상 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>프로세스 도중 오류가 발생했습니다. 오류는 애플리케이션이 다음에 수행할 수 있는 작업에도 영향을 줄 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 프로세스에 대한 피드백을 제공하거나(예를 들어, 다음 상태 변경을 기다리는 동안 회전기) 다음 메서드를 호출하기 전에 적절한 상태를 기다리는 등, 미디어 재생의 다음 단계를 수행할 수 있습니다.
