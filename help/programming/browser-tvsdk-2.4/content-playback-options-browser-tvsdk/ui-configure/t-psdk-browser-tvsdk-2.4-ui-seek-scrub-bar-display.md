---
description: 브라우저 TVSDK에서 스트림의 특정 위치(시간)를 찾을 수 있습니다. 스트림은 슬라이딩 윈도우 플레이리스트 또는 VOD(video-on-demand) 콘텐츠일 수 있습니다.
title: 검색 창 사용 시 검색 처리
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 검색 창 사용 시 검색 처리{#handle-seek-when-using-the-seek-bar}

브라우저 TVSDK에서 스트림의 특정 위치(시간)를 찾을 수 있습니다. 스트림은 슬라이딩 윈도우 플레이리스트 또는 VOD(video-on-demand) 콘텐츠일 수 있습니다.

>[!IMPORTANT]
>
>라이브 스트림에서의 찾기는 DVR에만 허용됩니다.

1. 브라우저 TVSDK가 올바른 찾기 상태 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 정지됨 및 재생입니다. 유효한 상태이면 미디어 리소스가 성공적으로 로드되었는지 확인합니다. 플레이어가 검색할 수 있는 올바른 상태가 아니면 다음 메서드를 호출하려고 하면 `IllegalStateException`.

   예를 들어 브라우저 TVSDK가 트리거될 때까지 기다릴 수 있습니다  `AdobePSDK.MediaPlayerStatusChangeEvent`  다음 포함 `event.status` / `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. 요청한 찾기 위치를 `MediaPlayer.seek` 메서드를 매개 변수로 사용합니다(밀리초).

   이렇게 하면 재생 헤드가 스트림의 다른 위치로 이동합니다.

   >[!TIP]
   >
   >요청된 찾기 위치가 실제 계산된 위치와 일치하지 않을 수 있습니다.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 브라우저 TVSDK가  `AdobePSDK.PSDKEventType.SEEK_END`  이벤트: 이벤트의 조정된 위치 반환 `actualPosition` 특성:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   이것은 검색 후의 실제 시작 위치가 요청된 위치와 다를 수 있기 때문에 중요하다. 다음 규칙 중 일부가 적용될 수 있습니다.

   * 검색 또는 기타 위치 재지정이 광고 브레이크 중간에 끝나거나 광고 브레이크를 건너뛸 경우 재생 비헤이비어가 영향을 받습니다.
   * 에셋의 검색 가능한 기간에서만 검색할 수 있습니다. VOD의 경우 0부터 자산 기간까지입니다.

1. 위의 예에서 만든 seekbar에 대해 다음을 들어보십시오. `setPositionChangeListener()` 사용자가 스크러빙하는 시간을 확인하려면:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. 사용자의 찾기 활동 변경에 대한 이벤트 리스너 콜백을 설정합니다.

       검색 작업은 비동기적이므로 Browser TVSDK는 검색과 관련된 다음 이벤트를 전달합니다.
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 찾기가 시작되고 있음을 나타냅니다.
   * `AdobePSDK.PSDKEventType.SEEK_END` 찾기가 성공했음을 나타냅니다.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 미디어 플레이어가 사용자가 제공한 찾기 위치를 재조정했음을 나타냅니다.
