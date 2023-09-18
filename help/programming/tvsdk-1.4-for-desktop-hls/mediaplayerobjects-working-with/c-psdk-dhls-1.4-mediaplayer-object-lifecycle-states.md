---
description: MediaPlayer 인스턴스를 생성하는 순간부터 인스턴스를 종료(재사용 또는 제거)하는 순간까지 이 인스턴스는 상태 간의 일련의 전환을 완료합니다.
title: MediaPlayer 개체 수명 주기
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# MediaPlayer 개체 수명 주기{#mediaplayer-object-lifecycle}

MediaPlayer 인스턴스를 생성하는 순간부터 인스턴스를 종료(재사용 또는 제거)하는 순간까지 이 인스턴스는 상태 간의 일련의 전환을 완료합니다.

일부 작업은 플레이어가 특정 상태에 있을 때만 허용됩니다. 예: 호출 `play` IDLE에서는 허용되지 않습니다. 플레이어가 PREPARED 상태에 도달한 후에만 이 상태를 호출할 수 있습니다.

상태로 작업하려면

* 의 현재 상태를 가져올 수 있습니다. `MediaPlayer` 을 사용하여 개체 `MediaPlayer.status` 속성.

  ```
  function get status():String;
  ```

* 상태 목록은에 정의되어 있습니다. `MediaPlayer.PlayerStatus`.

의 라이프사이클에 대한 상태 전환 다이어그램 `MediaPlayer` 인스턴스:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

다음 표에는 추가 세부 정보가 나와 있습니다.

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus </span> </th> 
   <th colname="col2" class="entry"> 다음과 같은 경우 발생 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 유휴 상태 </span> </td> 
   <td colname="col2"> <p> 응용 프로그램에서 인스턴스화하여 새 미디어 플레이어를 요청했습니다. <span class="codeph"> MediaPlayer </span>. 새로 만든 플레이어가 미디어 플레이어 항목 지정을 기다리고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 초기화 중 </span> </td> 
   <td colname="col2"> <p>애플리케이션 호출됨 <span class="codeph"> MediaPlayer.replaceCurrentResource </span>, 미디어 플레이어를 로드하는 중입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 초기화됨 </span> </td> 
   <td colname="col2"> <p>TVSDK가 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 준비 중 </span> </td> 
   <td colname="col2"> <p>애플리케이션 호출됨 <span class="codeph"> MediaPlayer.prepareToPlay </span>. 미디어 플레이어가 미디어 플레이어 항목 및 관련 리소스를 로드하는 중입니다. </p> <p>팁: 기본 미디어의 버퍼링이 발생할 수 있습니다. </p> <p>TVSDK가 미디어 스트림을 준비하고 광고 해결 및 광고 삽입(활성화된 경우)을 수행하려고 합니다. </p> <p>팁: 시작 시간을 0이 아닌 값으로 설정하려면 를 호출하십시오. <span class="codeph"> prepareToPlay(startTime) </span> 과 함께 사용할 수 있습니다(단위: 밀리초). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 준비됨 </span> </td> 
   <td colname="col2"> <p>콘텐츠가 준비되었고 광고가 타임라인에 삽입되었거나 광고 절차가 실패했습니다. 버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 재생 중 </span> </td> 
   <td colname="col2"> <p>애플리케이션이 을(를) 호출했습니다. <span class="codeph"> play </span>따라서 TVSDK에서 비디오를 재생하려고 합니다. 일부 버퍼링은 비디오가 실제로 재생되기 전에 발생할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 일시 중지됨 </span> </td> 
   <td colname="col2"> <p>애플리케이션이 미디어를 재생하고 일시 중지하면 미디어 플레이어가 이 상태와 재생 중 간을 이동합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 찾기 </span> </td> 
   <td colname="col2"> <p>일시 중지 또는 재생 도중 미디어 플레이어가 올바른 위치를 찾고 있습니다. 찾기가 시작되거나 종료되는 시기를 확인하려면 <span class="codeph"> SeekEvent.SEEK_BEGIN </span> 및 <span class="codeph"> SeekEvent.SEEK_END </span> 이벤트. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 완료됨 </span> </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달하여 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 릴리스됨 </span> </td> 
   <td colname="col2"> <p>애플리케이션이 미디어 플레이어를 릴리스했습니다. 또한 연결된 리소스를 릴리스합니다. 이 인스턴스를 더 이상 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 오류 </span> </td> 
   <td colname="col2"> <p>프로세스 도중 오류가 발생했습니다. 오류는 애플리케이션이 다음에 수행할 수 있는 작업에도 영향을 줄 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 프로세스에 대한 피드백을 제공하거나(예를 들어, 다음 상태 변경을 기다리는 동안 회전기) 다음 메서드를 호출하기 전에 적절한 상태를 기다리는 등, 미디어 재생의 다음 단계를 수행할 수 있습니다.
