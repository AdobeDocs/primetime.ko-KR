---
description: Browser TVSDK에서는 스트림의 특정 위치(시간)를 찾을 수 있습니다. 스트림은 슬라이딩 윈도우 재생 목록 또는 VOD(Video-On-Demand) 컨텐츠일 수 있습니다.
seo-description: Browser TVSDK에서는 스트림의 특정 위치(시간)를 찾을 수 있습니다. 스트림은 슬라이딩 윈도우 재생 목록 또는 VOD(Video-On-Demand) 컨텐츠일 수 있습니다.
seo-title: 검색 막대를 사용할 때 검색 처리
title: 검색 막대를 사용할 때 검색 처리
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 검색 막대를 사용할 때 검색 처리{#handle-seek-when-using-the-seek-bar}

Browser TVSDK에서는 스트림의 특정 위치(시간)를 찾을 수 있습니다. 스트림은 슬라이딩 윈도우 재생 목록 또는 VOD(Video-On-Demand) 컨텐츠일 수 있습니다.

>[!IMPORTANT]
>
>라이브 스트림에서 검색은 DVR에만 허용됩니다.

1. 브라우저 TV SDK가 유효한 검색 상태를 유지할 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 중지 및 재생됩니다. 유효한 상태이면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 올바른 검색 가능 상태가 아니면 다음 메서드를 호출하려고 하면 오류가 발생합니다 `IllegalStateException`.

   예를 들어 브라우저 TVSDK가 트리거될 때까지 `AdobePSDK.MediaPlayerStatusChangeEvent` 기다릴 수 `event.status` 있습니다 `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. 요청된 검색 위치를 `MediaPlayer.seek` 메서드로 밀리초 단위로 전달합니다.

   그러면 재생 헤드가 스트림의 다른 위치로 이동합니다.

   >[!TIP]
   >
   >요청된 검색 위치가 실제 계산된 위치와 일치하지 않을 수 있습니다.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 브라우저 TV SDK가 이벤트를 트리거할 때까지 기다리십시오. 그러면 이벤트의 속성에 조정된 위치가 `AdobePSDK.PSDKEventType.SEEK_END` `actualPosition` 반환됩니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   검색 후의 실제 시작 위치가 요청된 위치와 다를 수 있으므로 중요합니다. 다음 규칙 중 일부가 적용될 수 있습니다.

   * 재생 동작은 검색 또는 다른 위치 지정이 광고 중단 중간에 종료되거나 광고 분기를 건너뛰는 경우에 영향을 받습니다.
   * 자산의 검색 가능한 기간에서만 검색할 수 있습니다. VOD의 경우, 0부터 자산의 지속 시간입니다.

1. 위 예에서 만든 검색 막대의 경우 사용자가 스크러빙 중인 시간을 확인할 수 `setPositionChangeListener()` 있습니다.

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

1. 사용자의 검색 활동 변경 사항에 대한 이벤트 리스너 콜백을 설정합니다.

       검색 작업은 비동기식으로 이루어지므로 Browser TVSDK는 검색과 관련된 다음 이벤트를 전달합니다.
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 를 클릭하여 검색이 시작되고 있음을 나타냅니다.
   * `AdobePSDK.PSDKEventType.SEEK_END` 를 참조하십시오.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 사용자가 제공한 검색 위치를 재조정했음을 나타냅니다.

