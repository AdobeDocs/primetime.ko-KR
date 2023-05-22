---
description: TVSDK는 VOD(video on demand) 및 라이브 스트림에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.
title: 현재 재생 위치에 검색 스크러빙 막대 표시
exl-id: fb1a87ec-30ab-4dbe-9744-720eac523542
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 현재 재생 위치에 검색 스크러빙 막대 표시 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK는 VOD(video on demand) 및 라이브 스트림에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.

>[!TIP]
>
>라이브 스트림에서의 찾기는 DVR에만 허용됩니다.

1. 찾기를 위한 콜백을 설정합니다.

       찾기는 비동기적이므로 TVSDK는 다음 찾기 관련 이벤트를 전달합니다.
   
   * `MediaPlayerEvent.SEEK_BEGIN`: 찾기가 시작되는 위치입니다.
   * `MediaPlayerEvent.SEEK_END`: 찾기가 성공한 경우입니다.
   * `MediaPlayerEvent.OPERATION_FAILED`: 찾기가 실패한 경우입니다.

1. 플레이어가 찾기에 유효한 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 정지됨 및 재생입니다.
1. 기본 사용 `SeekBar` 설정 `OnSeekBarChangeListener`: 사용자가 스크러빙하는 시기를 결정합니다.
1. 요청한 찾기 위치(밀리초)를 `MediaPlayer.seek` 메서드를 사용합니다.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   에셋의 검색 가능한 기간에서만 검색할 수 있습니다. 온디맨드 비디오의 경우 0부터 자산 기간까지 입니다.

   >[!TIP]
   >
   >이 단계에서는 재생 헤드를 스트림의 새 위치로 이동하지만, 최종 계산된 위치가 지정된 검색 위치와 다를 수 있습니다.

1. 잘 들어 `MediaPlayerEvent.OPERATION_FAILED` 적절한 조치를 취하십시오.

   이 이벤트는 적절한 경고를 전달합니다. 애플리케이션이 진행 방법을 결정하며, 옵션에는 다시 찾기 시도 또는 이전 위치에서 재생 계속 등이 있습니다.

1. TVSDK가 `MediaPlayerEvent.SEEK_END` callback.
1. 콜백의 position 매개 변수를 사용하여 최종 조정된 재생 위치를 검색합니다.

   이것은 중요한 이유는 탐색 후의 실제 시작 위치가 요청된 위치와 다를 수 있기 때문이다. 검색 또는 기타 위치 변경이 광고 브레이크 중간에 종료되거나 광고 브레이크를 건너뛸 경우 재생 비헤이비어를 포함한 규칙이 적용될 수 있습니다.

1. 찾기 스크러빙 막대를 표시할 때 위치 정보를 사용합니다.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**찾기 사례**

이 예에서, 사용자는 원하는 위치로 이동하기 위해 탐색 바를 탐색한다.

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
