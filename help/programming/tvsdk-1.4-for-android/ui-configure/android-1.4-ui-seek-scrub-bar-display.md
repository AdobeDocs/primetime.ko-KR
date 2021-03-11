---
description: TVSDK는 스트림이 VOD(Video On Demand) 및 실시간 스트림에서 슬라이딩 윈도우 재생 목록인 특정 위치(시간)로의 검색을 지원합니다.
title: 현재 재생 위치에 검색 스크러빙 막대 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 현재 재생 위치 {#display-a-seek-scrub-bar-with-the-current-playback-position}에 검색 스크러빙 막대를 표시합니다.

TVSDK는 스트림이 VOD(Video On Demand) 및 실시간 스트림에서 슬라이딩 윈도우 재생 목록인 특정 위치(시간)로의 검색을 지원합니다.

>[!IMPORTANT]
>
>라이브 스트림에서 검색은 DVR에만 허용됩니다.

1. 검색을 위한 콜백을 설정합니다.

       검색은 비동기식이므로 TVSDK는 다음과 같은 검색 관련 이벤트를 전달합니다.
   
   * `QOSEventListener.onSeekStart` - 시작을 찾습니다.
   * `QOSEventListener.onSeekComplete` - 성공적으로 검색
   * `QOSEventListener.onOperationFailed` - 검색하지 못했습니다.

1. 플레이어가 검색을 위해 유효한 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 중지됨 및 재생됩니다.

1. 기본 SeekBar를 사용하여 사용자가 스크러빙하는 시간을 확인할 수 있도록 `OnSeekBarChangeListener`을 설정합니다.
1. `QOSEventListener.onOperationFailed`에 귀 기울이고 적절한 작업을 수행합니다.

   이 이벤트는 적절한 경고를 전달합니다. 예를 들어, 응용 프로그램에서 검색을 다시 시도하거나 이전 위치에서 재생을 계속 진행하도록 하는 방법을 결정합니다.

1. TVSDK가 `QOSEventListener.onSeekComplete` 콜백을 호출할 때까지 기다립니다.
1. 콜백의 위치 매개 변수를 사용하여 마지막으로 조정된 재생 위치를 검색합니다.

   검색 후 실제 시작 위치가 요청된 위치와 다를 수 있으므로 이 작업은 중요합니다. 검색 또는 다른 위치 지정이 광고 브레이크 중간에 종료되거나 광고 분리를 건너뛰면 재생 비헤이비어가 영향을 받을 수 있습니다.

1. 검색 스크러빙 막대를 표시할 때 위치 정보를 사용합니다.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**검색 예**

이 예에서 사용자는 검색 막대를 스크럽하여 원하는 위치를 찾습니다.

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
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

