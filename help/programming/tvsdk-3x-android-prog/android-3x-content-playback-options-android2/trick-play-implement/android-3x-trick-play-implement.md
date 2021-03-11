---
description: 사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정합니다.
title: 빨리 전달 및 되감기 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 개요 {#implement-fast-forward-and-rewind}

사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정합니다.

속도를 전환하려면 하나의 값을 설정해야 합니다.

1. `MediaPlayer`의 속도를 허용된 값으로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다.

       다음 정보를 기억하십시오.
   
   * `MediaPlayerItem` 클래스는 허용되는 재생 속도를 정의합니다.
   * 지정된 요금이 허용되지 않을 경우 TVSDK에서 허용된 가장 가까운 비율을 선택합니다.

      다음 예제에서는 플레이어의 내부 재생 속도를 요청된 속도로 설정합니다.

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. 비율 변경을 요청할 때와 비율 변경이 실제로 발생할 때 알려 주는 비율 변경 이벤트를 선택적으로 수신할 수 있습니다.

TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.

* `MediaPlayerEvent.RATE_SELECTED`으로  `rate` 변경할 수 있습니다.

* `MediaPlayerEvent.RATE_PLAYING`를 클릭하여 선택한 속도로 재생을 재개할 수 있습니다.

   TVSDK는 플레이어가 트릭 재생 모드에서 일반 재생 모드로 돌아오면 이러한 이벤트를 전달합니다.