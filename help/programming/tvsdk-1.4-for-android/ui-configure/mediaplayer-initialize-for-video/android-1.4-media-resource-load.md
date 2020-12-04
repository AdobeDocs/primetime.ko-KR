---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-title: MediaPlayer에서 미디어 리소스 로드
title: MediaPlayer에서 미디어 리소스 로드
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 4ef05be045334a2e723da4c7c6a7ee22fb0f776c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# MediaPlayer {#load-a-media-resource-in-the-mediaplayer}에서 미디어 리소스 로드

MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 재생할 새 리소스로 Media Player의 재생 가능한 항목을 설정합니다.

   `MediaPlayer.replaceCurrentItem`을(를) 호출하고 기존 `MediaResource` 인스턴스를 전달하여 기존 Media Player의 현재 재생 가능한 항목을 교체합니다.

1. `MediaPlayer.PlaybackEventListener` 인터페이스의 구현을 `MediaPlayer` 인스턴스와 등록합니다.

   * `onPrepared`
   * `onStateChanged`, and check for INITIALIZED and ERROR.

1. 미디어 플레이어의 상태가 INITIALIZED로 변경되면 `MediaPlayer.prepareToPlay`을 호출할 수 있습니다

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. `prepareToPlay`을(를) 호출하면 광고 해상도 및 배치 프로세스가 시작됩니다.

1. TVSDK가 `onPrepared` 콜백을 호출하면 미디어 스트림이 성공적으로 로드되고 재생될 준비가 됩니다.

   미디어 스트림이 로드되면 `MediaPlayerItem`이(가) 만들어집니다.

>오류가 발생하면 `MediaPlayer`은 ERROR 상태로 전환됩니다. 또한 `PlaybackEventListener.onStateChanged`콜백을 호출하여 응용 프로그램에 알립니다.
>
>이 프로세스에서는 다음과 같은 여러 매개 변수를 전달합니다.
>* `MediaPlayer.PlayerState.ERROR` 값이 있는 `MediaPlayer.PlayerState` 유형의 `state` 매개 변수입니다.
   >
   >
* 오류 이벤트에 대한 진단 정보를 포함하는 `MediaPlayerNotification` 유형의 `notification` 매개 변수입니다.


다음 간소화된 샘플 코드는 미디어 리소스를 로드하는 프로세스를 보여 줍니다.

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
