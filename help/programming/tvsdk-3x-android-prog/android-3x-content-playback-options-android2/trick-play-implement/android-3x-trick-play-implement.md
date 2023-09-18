---
description: 사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정합니다.
title: 신속한 전달 및 되감기 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 개요 {#implement-fast-forward-and-rewind}

사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정합니다.

속도를 전환하려면 하나의 값을 설정해야 합니다.

1. 속도를 로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다. `MediaPlayer` 을 입력합니다.

       다음 정보를 숙지하십시오.
   
   * 다음 `MediaPlayerItem` 클래스는 허용된 재생 속도를 정의합니다.
   * TVSDK는 지정된 속도가 허용되지 않는 경우 가장 가까운 허용 속도를 선택합니다.

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

1. 선택적으로 비율 변경을 요청했을 때와 비율 변경이 실제로 발생하는 시기를 알리는 비율 변경 이벤트를 수신할 수 있습니다.

TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.

* `MediaPlayerEvent.RATE_SELECTED`, 다음과 같은 경우 `rate` 값이 다른 값으로 변경됩니다.

* `MediaPlayerEvent.RATE_PLAYING`: 선택한 속도로 재생이 다시 시작되는 때입니다.

  TVSDK는 플레이어가 트릭 재생 모드에서 일반 재생 모드로 돌아가면 이러한 이벤트를 전달합니다.
