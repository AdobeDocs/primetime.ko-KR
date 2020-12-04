---
description: TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.
seo-description: TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.
seo-title: 비디오 지속 시간, 현재 시간 및 남은 시간 표시
title: 비디오 지속 시간, 현재 시간 및 남은 시간 표시
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 비디오{#display-the-duration-current-time-and-remaining-time-of-the-video}의 지속 시간, 현재 시간 및 남은 시간을 표시합니다.

TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.

1. 플레이어가 준비 상태가 될 때까지 기다립니다.
1. `MediaPlayer.getCurrentTime` 메서드를 사용하여 현재 재생 헤드 시간을 검색합니다.

   가상 타임라인에서 현재 재생 헤드 위치를 밀리초 단위로 반환합니다. 여러 광고나 광고 분리가 기본 스트림에 분할되는 등 대체 컨텐츠의 여러 인스턴스가 포함될 수 있는 해결된 스트림에 대해 시간을 계산합니다. 라이브/선형 스트림의 경우 반환된 시간은 항상 재생 창 범위에 있습니다.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 스트림의 재생 범위를 검색하고 지속 시간을 결정합니다.
   1. 가상 타임라인 시간 범위를 가져오려면 `mediaPlayer.getPlaybackRange` 메서드를 사용합니다.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. `mediacore.utils.TimeRange`을(를) 사용하여 시간 범위를 분석합니다.
   1. 지속 기간을 결정하려면 범위 끝에서 시작을 빼십시오.

      여기에는 스트림에 삽입되는 추가 컨텐츠 기간이 포함됩니다(광고).

      VOD의 경우 범위는 항상 0으로 시작하고 종료 값은 기본 컨텐츠 지속 기간의 합계와 스트림(광고)에 삽입된 추가 컨텐츠 지속 시간을 합한 것입니다.

      선형/라이브 에셋의 경우 범위는 재생 창 범위를 나타내며 이 범위는 재생 중에 변경됩니다.

      TVSDK는 `onUpdated` 콜백을 호출하여 미디어 항목을 새로 고치고 해당 속성(재생 범위 포함)이 업데이트되었음을 나타냅니다.

1. Android SDK에서 공개적으로 사용할 수 있는 `MediaPlayer` 및 `SeekBar` 클래스에서 사용할 수 있는 메서드를 사용하여 seek-bar 매개 변수를 설정합니다.

   예를 들어, 다음은 `SeekBar` 및 두 개의 `TextView` 요소를 포함하는 가능한 레이아웃입니다.

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

1. 타이머를 사용하여 현재 시간을 주기적으로 검색하고 SeekBar를 업데이트합니다.

   다음 예제에서는 참조 플레이어 PrimetimeReference에서 사용할 수 있는 타이머로 `Clock.java` 도우미 클래스를 사용합니다. 이 클래스는 이벤트 리스너를 설정하고 매 초마다 `onTick` 이벤트를 트리거하거나 지정할 수 있는 다른 시간 초과 값을 트리거합니다.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   이 예에서는 모든 시계 키트에서 미디어 플레이어의 현재 위치를 검색하고 SeekBar를 업데이트합니다. 두 TextView 요소를 사용하여 현재 시간과 재생 범위 종료 위치를 숫자 값으로 표시합니다.

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```

