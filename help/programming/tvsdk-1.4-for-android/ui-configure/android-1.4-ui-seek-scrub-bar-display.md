---
description: TVSDK는 VOD(video on demand) 및 라이브 스트림 모두에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.
title: 현재 재생 위치에 검색 스크러빙 막대 표시
exl-id: 8076521b-579d-491f-97de-c7b57daa9b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 현재 재생 위치에 검색 스크러빙 막대 표시 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK는 VOD(video on demand) 및 라이브 스트림 모두에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.

>[!IMPORTANT]
>
>라이브 스트림에서의 찾기는 DVR에만 허용됩니다.

1. 찾기를 위한 콜백을 설정합니다.

       찾기는 비동기적이므로 TVSDK는 다음 찾기 관련 이벤트를 전달합니다.
   
   * `QOSEventListener.onSeekStart` - 찾기 시작.
   * `QOSEventListener.onSeekComplete` - 검색 성공.
   * `QOSEventListener.onOperationFailed` - 찾기가 실패했습니다.

1. 플레이어가 찾기에 유효한 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 정지됨 및 재생입니다.

1. 기본 SeekBar를 사용하여 `OnSeekBarChangeListener` 을 클릭하여 사용자가 스크러빙하는 시간을 확인합니다.
1. 잘 들어 `QOSEventListener.onOperationFailed` 적절한 조치를 취하십시오.

   이 이벤트는 적절한 경고를 전달합니다. 예를 들어 애플리케이션은 검색을 다시 시도하거나 이전 위치에서 재생을 계속함으로써 진행 방법을 결정합니다.

1. TVSDK가 `QOSEventListener.onSeekComplete` callback.
1. 콜백의 position 매개 변수를 사용하여 최종 조정된 재생 위치를 검색합니다.

   이것은 중요한 이유는 탐색 후의 실제 시작 위치가 요청된 위치와 다를 수 있기 때문이다. 검색 또는 기타 위치 변경이 광고 브레이크 중간에 끝나거나 광고 브레이크를 건너뛸 경우 재생 동작이 영향을 받을 수 있습니다.

1. 찾기 스크러빙 막대를 표시할 때 위치 정보를 사용합니다.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**찾기 사례**

이 예에서, 사용자는 원하는 위치로 이동하기 위해 탐색 바를 탐색한다.

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
