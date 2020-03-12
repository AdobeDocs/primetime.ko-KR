---
description: TVSDK는 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)와 VOD(Video On Demand) 및 실시간 스트림을 검색할 수 있도록 지원합니다.
seo-description: TVSDK는 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)와 VOD(Video On Demand) 및 실시간 스트림을 검색할 수 있도록 지원합니다.
seo-title: 현재 재생 위치로 검색 스크럽 막대 표시
title: 현재 재생 위치로 검색 스크럽 막대 표시
uuid: df045a10-8d74-4874-8fa5-7e9571c8678d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 현재 재생 위치로 검색 스크럽 막대 표시 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK는 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)와 VOD(Video On Demand) 및 실시간 스트림을 검색할 수 있도록 지원합니다.

>[!TIP]
>
>라이브 스트림에서의 검색은 DVR에 대해서만 허용됩니다.

1. 검색을 위한 콜백을 설정합니다.

       검색은 비동기식이므로 TVSDK는 다음과 같은 검색 관련 이벤트를 전달합니다.
   
   * `MediaPlayerEvent.SEEK_BEGIN`를 선택합니다.
   * `MediaPlayerEvent.SEEK_END`를 찾습니다.
   * `MediaPlayerEvent.OPERATION_FAILED`가 아닌 경우.

1. 플레이어가 유효한 검색 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 중지됨 및 재생입니다.
1. 기본 설정을 `SeekBar` 사용하여 사용자가 스크러빙 `OnSeekBarChangeListener`중인 시기를 결정합니다.
1. 요청된 검색 위치(밀리초)를 `MediaPlayer.seek` 메서드에 전달합니다.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   자산의 검색 가능한 기간에서만 검색할 수 있습니다. On-Demand 비디오의 경우 0부터 자산의 지속 시간입니다.

   >[!TIP]
   >
   >이 단계에서는 재생 헤드를 스트림의 새 위치로 이동하지만 최종 계산된 위치는 지정된 검색 위치와 다를 수 있습니다.

1. 경청하고 적절한 `MediaPlayerEvent.OPERATION_FAILED` 조치를 취하십시오.

   이 이벤트는 적절한 경고를 전달합니다. 응용 프로그램에서 진행 방법을 결정하며 옵션에는 검색 다시 시도 또는 이전 위치에서 계속 재생되는 작업이 포함됩니다.

1. TVSDK가 콜백을 호출할 때까지 `MediaPlayerEvent.SEEK_END` 기다립니다.
1. 콜백의 위치 매개 변수를 사용하여 마지막으로 조정된 재생 위치를 검색합니다.

   검색 후 실제 시작 위치가 요청된 위치와 다를 수 있으므로 중요합니다. 검색 또는 다른 위치 지정이 광고 중단 중간에 종료되거나 광고 분리를 건너뛰면 재생 동작을 비롯한 규칙이 적용됩니다.

1. 검색 스크럽 막대를 표시할 때 위치 정보를 사용합니다.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**검색 예**

이 예에서 사용자는 검색 막대를 스크럽하여 원하는 위치를 찾습니다.

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()), 
        playbackRange.getDuration()); 
     
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```

