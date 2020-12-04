---
description: 인스턴트 온(instant on) 용어는 하나 이상의 채널을 미리 로드하여 채널을 선택하거나 채널을 전환하는 사용자가 컨텐츠를 즉시 재생하도록 하는 것을 의미합니다. 버퍼링은 사용자가 시청을 시작할 때까지 이미 수행됩니다.
seo-description: 인스턴트 온(instant on) 용어는 하나 이상의 채널을 미리 로드하여 채널을 선택하거나 채널을 전환하는 사용자가 컨텐츠를 즉시 재생하도록 하는 것을 의미합니다. 버퍼링은 사용자가 시청을 시작할 때까지 이미 수행됩니다.
seo-title: 즉시 사용
title: 즉시 사용
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# {#instant-on}에 인스턴트

인스턴트 온(instant on) 용어는 하나 이상의 채널을 미리 로드하여 채널을 선택하거나 채널을 전환하는 사용자가 컨텐츠를 즉시 재생하도록 하는 것을 의미합니다. 버퍼링은 사용자가 시청을 시작할 때까지 이미 수행됩니다.

TVSDK는 즉시 켜지지 않고 재생될 미디어를 초기화하지만 응용 프로그램이 `play`을 호출하기 전까지 스트림을 버퍼링하지 않습니다. 버퍼링이 완료될 때까지 사용자에게 컨텐츠가 표시되지 않습니다. 즉시 켜짐으로 여러 미디어 플레이어(또는 미디어 플레이어 항목 로더) 인스턴스를 실행할 수 있으며 TVSDK가 스트림을 즉시 버퍼링하기 시작합니다.

사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 `play`을(를) 호출하면 즉시 재생이 시작됩니다.

TVSDK가 실행할 수 있는 `MediaPlayer` 인스턴스 수에 대한 제한은 없지만, 더 많은 인스턴스를 실행하면 더 많은 리소스가 소모됩니다. 실행 중인 인스턴스 수의 애플리케이션 성능에 영향을 줄 수 있습니다. 이러한 인스턴스에 대한 자세한 내용은 [MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)를 사용하여 미디어 리소스 로드를 참조하십시오.

## 즉각적인 재생을 위한 버퍼링 구성 {#configure-buffering-for-instant-on-playback}

사용자는 즉시 채널을 전환할 수 있고, 대기 시간이 없는 즉시 재생을 시작할 수 있습니다. 즉시 켜기를 활성화하면 TVSDK가 재생을 시작하기 전에 하나 이상의 채널을 버퍼링합니다.

1. 리소스가 로드되었고 상태가 PREMITED인지 확인하여 재생할 준비가 되었는지 확인합니다.
1. `play`을(를) 호출하기 전에 각 `MediaPlayer` 인스턴스에 대해 `prepareBuffer`을(를) 호출합니다.

   이렇게 하면 TVSDK가 실제로 미디어 리소스를 재생하지 않고 버퍼링을 시작합니다. 버퍼가 가득 차면 TVSDK가 `BUFFERING_COMPLETED` 이벤트를 전달합니다.

   >[!NOTE]
   >
   >기본적으로 `prepareBuffer` 및 `prepareToPlay`은 미디어 스트림을 설정하여 처음부터 재생을 시작합니다. 다른 위치에서 시작하려면 위치(밀리초)를 `prepareToPlay`으로 전달합니다.

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

1. `BUFFERING_COMPLETE` 이벤트를 받으면 항목 재생을 시작하거나 컨텐츠가 완전히 버퍼링되었음을 나타내는 시각적 피드백을 표시합니다.

   `play`을(를) 호출하는 경우 재생을 즉시 시작해야 합니다.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
