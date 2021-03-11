---
description: TVSDK를 사용하여 미디어 상의 플레이어의 위치에 대한 정보를 검색하고 검색 표시줄에 표시할 수 있습니다.
title: 비디오 지속 시간, 현재 시간 및 남은 시간 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 비디오 {#display-the-duration-current-time-and-remaining-time-of-the-video} 지속 시간, 현재 시간 및 남은 시간 표시

TVSDK를 사용하여 미디어 상의 플레이어의 위치에 대한 정보를 검색하고 검색 표시줄에 표시할 수 있습니다.

1. 플레이어가 준비 상태 이상 될 때까지 기다립니다.
1. `MediaPlayer.getCurrentTime` 메서드를 사용하여 현재 재생 헤드 시간을 검색합니다.

   가상 타임라인의 현재 재생 헤드 위치를 밀리초 단위로 반환합니다. 여러 광고 또는 광고가 기본 스트림에 분할되는 등 대체 컨텐츠의 여러 인스턴스가 포함될 수 있는 해결된 스트림에 대해 시간을 계산합니다. 실시간/선형 스트림의 경우, 반환된 시간은 항상 재생 창 범위에 있습니다.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 스트림의 재생 범위를 검색하고 지속 시간을 결정합니다.
   1. 가상 타임라인 시간 범위를 가져오려면 `MediaPlayer.getPlaybackRange` 메서드를 사용합니다.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 가상 타임라인 시간 범위를 가져오려면 `MediaPlayer.getPlaybackRange` 메서드를 사용합니다.

      * VOD의 경우 범위는 항상 0으로 시작하고 종료 값은 기본 컨텐츠 지속 기간의 합계와 스트림(광고)의 추가 컨텐츠 지속 시간을 합한 것입니다.
      * 선형/라이브 자산의 경우 범위는 재생 창 범위를 나타냅니다. 재생하는 동안 이 범위가 변경됩니다.

         TVSDK는 `ITEM_Updated` 콜백을 호출하여 미디어 항목이 새로 고쳐졌고 재생 범위를 비롯한 해당 속성이 업데이트되었음을 나타냅니다.

1. Android SDK의 `MediaPlayer` 및 `SeekBar` 클래스에서 사용할 수 있는 메서드를 사용하여 seek-bar 매개 변수를 설정합니다.

   예를 들어, 검색 막대와 두 개의 `TextView` 요소를 포함하는 가능한 레이아웃이 있습니다.

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. 그림에 표시된 대로 타이머를 사용하여 현재 시간을 정기적으로 검색하고 검색 막대를 업데이트합니다.

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   다음 예제에서는 `ReferencePlayer`에서 사용할 수 있는 `Clock.java` 도우미 클래스를 타이머로 사용합니다. 이 클래스는 이벤트 리스너를 설정하고 매 초마다 `onTick` 이벤트 또는 지정할 수 있는 다른 시간 초과 값을 트리거합니다.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   이 예제는 모든 시계 확인 시 미디어 플레이어의 현재 위치를 검색하고 검색 막대를 업데이트합니다. 두 개의 `TextView` 요소를 사용하여 현재 시간과 재생 범위 종료 위치를 숫자 값으로 표시합니다.

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
