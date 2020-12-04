---
description: 사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 플레이 모드에 있는 것입니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.
seo-description: 사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 플레이 모드에 있는 것입니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.
seo-title: 신속하게 전달 및 되감기
title: 신속하게 전달 및 되감기
uuid: 2e5d0fd0-0290-4f08-b9c6-c8ecde26abb8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 개요 {#implement-fast-forward-and-rewind-overview}

사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 플레이 모드에 있는 것입니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.

속도를 전환하려면 하나의 값을 설정해야 합니다.

1. `MediaPlayer`의 속도를 허용된 값으로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다.

   * `MediaPlayerItem` 클래스는 허용되는 재생 속도를 정의합니다.
   * 지정된 요금이 허용되지 않을 경우 TVSDK에서 가장 가까운 허용 비율을 선택합니다.

   이 예에서는 플레이어의 내부 재생 속도를 요청된 속도로 설정합니다.

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. 비율 변경을 요청할 때와 환율 변경이 실제로 발생하는 시기를 알려주는 비율 변경 이벤트를 선택적으로 수신할 수 있습니다.

       TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 값을 다른 값으로  `rate` 변경하는 경우.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 선택한 속도로 재생을 재개할 수 있습니다.

      TVSDK는 플레이어가 트릭 플레이 모드에서 일반 재생 모드로 돌아갈 때 이러한 두 이벤트를 전달합니다.

