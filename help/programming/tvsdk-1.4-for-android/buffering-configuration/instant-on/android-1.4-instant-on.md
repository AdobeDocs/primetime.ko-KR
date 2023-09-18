---
description: 인스턴트 온이라는 용어는 하나 이상의 채널을 미리 로드하여 사용자가 채널을 선택하거나 채널을 전환하면 콘텐츠가 즉시 재생되는 것을 볼 수 있도록 하는 것을 말합니다. 버퍼링은 사용자가 시청을 시작할 때까지 이미 수행됩니다.
title: 인스턴트 켜짐
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 인스턴트 켜짐 {#instant-on}

인스턴트 온이라는 용어는 하나 이상의 채널을 미리 로드하여 사용자가 채널을 선택하거나 채널을 전환하면 콘텐츠가 즉시 재생되는 것을 볼 수 있도록 하는 것을 말합니다. 버퍼링은 사용자가 시청을 시작할 때까지 이미 수행됩니다.

즉시 켜지 않으면 TVSDK는 재생할 미디어를 초기화하지만 애플리케이션이 호출될 때까지 스트림 버퍼링을 시작하지 않습니다 `play`. 버퍼링이 완료될 때까지 콘텐츠가 표시되지 않습니다. 즉시 켜면 여러 미디어 플레이어(또는 미디어 플레이어 항목 로더) 인스턴스를 시작할 수 있으며 TVSDK는 즉시 스트림 버퍼링을 시작합니다.

사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 호출 `play` 새 채널에서 즉시 재생을 시작합니다.

의 수에는 제한이 없지만 `MediaPlayer` tvsdk가 실행할 수 있는 인스턴스는 더 많은 인스턴스를 실행하므로 더 많은 리소스를 사용합니다. 실행 중인 인스턴스 수에 따라 응용 프로그램 성능이 영향을 받을 수 있습니다. 이러한 인스턴스에 대한 자세한 내용은 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## 인스턴트 온 재생을 위한 버퍼링 구성 {#configure-buffering-for-instant-on-playback}

즉시 켜면 사용자는 채널을 전환할 수 있으며 대기 시간 없이 즉시 재생이 시작됩니다. 인스턴트 온 기능을 활성화하면 재생이 시작되기 전에 TVSDK가 하나 이상의 채널을 버퍼링합니다.

1. 상태가 PREPARED인지 확인하여 리소스가 로드되었고 재생할 준비가 되었는지 확인합니다.
1. 호출 전 `play`, 호출 `prepareBuffer` 각 `MediaPlayer` 인스턴스.

   이렇게 하면 즉시 사용할 수 있습니다. 즉, TVSDK가 미디어 리소스를 실제로 재생하지 않고 버퍼링을 시작합니다. TVSDK가 `BUFFERING_COMPLETED` 버퍼가 가득 찬 경우의 이벤트입니다.

   >[!NOTE]
   >
   >기본적으로, `prepareBuffer` 및 `prepareToPlay` 미디어 스트림을 설정하여 처음부터 재생을 시작합니다. 다른 위치에서 시작하려면 해당 위치(밀리초)를에 전달합니다. `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. 다음을 받을 때 `BUFFERING_COMPLETE` 이벤트가 발생하면 항목 재생을 시작하거나 콘텐츠가 완전히 버퍼링되었음을 나타내는 시각적 피드백을 표시합니다.

   전화 주시면 `play`, 재생이 즉시 시작됩니다.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
