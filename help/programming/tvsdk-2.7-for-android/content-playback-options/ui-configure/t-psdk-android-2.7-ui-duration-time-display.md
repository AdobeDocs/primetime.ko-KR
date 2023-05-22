---
description: TVSDK를 사용하여 미디어에서 플레이어의 위치에 대한 정보를 검색하고 찾기 표시줄에 표시할 수 있습니다.
title: 비디오의 지속 시간, 현재 시간 및 남은 시간을 표시합니다.
exl-id: d9832f19-c2d1-413a-b094-091052912c96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 비디오의 지속 시간, 현재 시간 및 남은 시간을 표시합니다. {#display-the-duration-current-time-and-remaining-time-of-the-video}

TVSDK를 사용하여 미디어에서 플레이어의 위치에 대한 정보를 검색하고 찾기 표시줄에 표시할 수 있습니다.

1. 플레이어가 적어도 PREPARED 상태가 될 때까지 기다립니다.
1. 를 사용하여 현재 플레이헤드 시간 검색 `MediaPlayer.getCurrentTime` 메서드를 사용합니다.

   이렇게 하면 가상 타임라인의 현재 플레이헤드 위치가 밀리초 단위로 반환됩니다. 이 시간은 기본 스트림에 여러 광고 또는 광고 브레이크와 같은 대체 콘텐츠의 여러 인스턴스를 포함할 수 있는 확인된 스트림을 기준으로 계산됩니다. 라이브/선형 스트림의 경우 반환되는 시간은 항상 재생 창 범위입니다.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 스트림의 재생 범위를 검색하고 지속 시간을 결정합니다.
   1. 사용 `MediaPlayer.getPlaybackRange` 메서드는 가상 타임라인 시간 범위를 가져옵니다.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 사용 `MediaPlayer.getPlaybackRange` 메서드는 가상 타임라인 시간 범위를 가져옵니다.

      * VOD의 경우 범위는 항상 0으로 시작하며 종료 값은 기본 콘텐츠 지속 시간과 스트림(광고)의 추가 콘텐츠 지속 시간의 합계와 같습니다.
      * 선형/라이브 에셋의 경우 범위는 재생 창 범위를 나타냅니다. 이 범위는 재생 중에 변경됩니다.

         TVSDK에서 `ITEM_Updated` 미디어 항목이 새로 고쳐졌고 재생 범위를 포함한 해당 특성이 업데이트되었음을 나타내는 콜백입니다.

1. 에서 사용할 수 있는 메서드 사용 `MediaPlayer` 및 `SeekBar` 클래스로 사용하여 Android SDK의 검색 창 매개 변수를 설정할 수 있습니다.

   예를 들어 검색 창과 2개를 포함하는 가능한 레이아웃이 여기에 있습니다 `TextView` 요소.

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

1. 타이머를 사용하여 그림과 같이 현재 시간을 주기적으로 검색하고 찾기 표시줄을 업데이트합니다.

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   다음 예제에서는 `Clock.java` 에서 사용할 수 있는 도우미 클래스 `ReferencePlayer`를 타이머로 사용하십시오. 이 클래스는 이벤트 리스너를 설정하고 `onTick` 매 초마다 이벤트 또는 지정할 수 있는 다른 시간 초과 값입니다.

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

   모든 시계 바늘에서 이 예제는 미디어 플레이어의 현재 위치를 검색하고 검색 막대를 업데이트합니다. 두 가지를 이용합니다 `TextView` 현재 시간 및 재생 범위 종료 위치를 숫자 값으로 표시하는 요소입니다.

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
