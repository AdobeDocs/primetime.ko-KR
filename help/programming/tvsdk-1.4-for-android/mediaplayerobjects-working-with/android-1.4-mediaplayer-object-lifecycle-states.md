---
description: MediaPlayer 인스턴스를 만드는 순간부터 종료(재사용 또는 제거)되는 순간까지 이 인스턴스는 상태 간 일련의 전환을 완료합니다.
seo-description: MediaPlayer 인스턴스를 만드는 순간부터 종료(재사용 또는 제거)되는 순간까지 이 인스턴스는 상태 간 일련의 전환을 완료합니다.
seo-title: MediaPlayer 객체 라이프사이클
title: MediaPlayer 객체 라이프사이클
uuid: 6670a30c-7053-4754-bc36-6bb8590c001d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer 객체 라이프사이클{#mediaplayer-object-lifecycle}

MediaPlayer 인스턴스를 만드는 순간부터 종료(재사용 또는 제거)되는 순간까지 이 인스턴스는 상태 간 일련의 전환을 완료합니다.

일부 작업은 플레이어가 특정 상태일 때만 허용됩니다. 예를 들어 `play` 인 호출은 `IDLE` 허용되지 않습니다. 플레이어가 `PREPARED` 상태에 도달한 후에만 이 상태를 호출할 수 있습니다.

상태를 사용하여 작업하려면

* 로 `MediaPlayer` 객체의 현재 상태를 검색할 수 `MediaPlayer.getStatus`있습니다.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* 상태 목록은 에 정의되어 `MediaPlayer.PlayerState`있습니다.

인스턴스 라이프사이클에 대한 상태 전환 다이어그램: `MediaPlayer`
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

다음 표에서는 추가 세부 사항을 제공합니다.

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> 다음 경우에 발생합니다. </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 유휴 </span> </td> 
   <td colname="col2"> <p>응용 프로그램에서 DefaultMediaPlayer.create를 호출하여 새 미디어 플레이어를 <span class="codeph"> 요청했습니다 </span>. 새로 만든 플레이어가 미디어 플레이어 항목을 지정하기를 기다리고 있습니다. 미디어 플레이어의 초기 상태입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 초기화 중 </span> </td> 
   <td colname="col2"> <p>MediaPlayer.replaceCurrentItem <span class="codeph"> 이라는 응용 프로그램을 </span>로드하고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 초기화됨 </span> </td> 
   <td colname="col2"> <p>TVSDK가 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 준비 </span> </td> 
   <td colname="col2"> <p>MediaPlayer.prepareToPlay <span class="codeph"> 라는 응용 프로그램이 </span>있습니다. 미디어 플레이어가 미디어 플레이어 항목 및 관련 리소스를 로드하고 있습니다. </p> <p>팁: 기본 미디어의 일부 버퍼링이 발생할 수 있습니다. </p> <p>TVSDK가 미디어 스트림을 준비하고 광고 확인 및 광고 삽입(활성화된 경우)을 수행하려고 합니다. </p> <p>팁: 시작 시간을 0이 아닌 값으로 설정하려면, <span class="codeph"> 준비 ToPlay(startTime) </span> 를 밀리초 단위로 호출합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 준비 완료 </span> </td> 
   <td colname="col2"> <p>컨텐츠가 준비되고 광고가 타임라인에 삽입되었거나 광고 절차가 실패했습니다. 버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 재생 </span> </td> 
   <td colname="col2"> <p>응용 프로그램이 <span class="codeph"> </span>play를 호출했으므로 TVSDK가 비디오를 재생하려고 합니다. 일부 버퍼링은 비디오가 실제로 재생되기 전에 발생할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 일시 중지됨 </span> </td> 
   <td colname="col2"> <p>애플리케이션이 미디어를 재생하거나 일시 중지하면 미디어 플레이어는 이 상태와 PLAYING 사이에서 이동합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 일시 중단 </span> </td> 
   <td colname="col2"> <p>플레이어가 재생되거나 일시 정지되는 동안 응용 프로그램이 재생을 중단하고 장치를 종료하거나 애플리케이션을 전환했습니다. 미디어 플레이어가 일시 중단되고 리소스가 해제되었습니다. 계속하려면 미디어 플레이어를 복원합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 완료 </span> </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달했으며 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 릴리스됨 </span> </td> 
   <td colname="col2"> <p>응용 프로그램에서 미디어 플레이어를 릴리스했습니다. 미디어 플레이어는 연결된 리소스도 릴리스합니다. 이 인스턴스를 더 이상 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 오류 </span> </td> 
   <td colname="col2"> <p>프로세스 중에 오류가 발생했습니다. 오류가 발생하면 다음에 응용 프로그램이 수행할 수 있는 작업도 영향을 받을 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 프로세스에 대한 피드백을 제공하거나(예: 다음 상태 변경을 기다리는 동안 스피너) 다음 방법을 호출하기 전에 적절한 상태를 기다리는 등의 미디어 재생 다음 단계를 수행할 수 있습니다.

예:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```

