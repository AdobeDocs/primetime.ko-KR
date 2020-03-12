---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-title: MediaPlayer에서 미디어 리소스 로드
title: MediaPlayer에서 미디어 리소스 로드
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer에서 미디어 리소스 로드 {#load-a-media-resource-in-the-mediaplayer}

MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 재생할 새 리소스로 MediaPlayer의 재생 가능한 항목을 설정합니다.

   기존 인스턴스를 호출하고 전달하여 기존 MediaPlayer의 현재 재생 가능한 항목을 `MediaPlayer.replaceCurrentItem` 교체합니다 `MediaResource` .

1. 인스턴스에 `MediaPlayer.PlaybackEventListener` 인터페이스 구현을 등록합니다 `MediaPlayer` .

   * `onPrepared`
   * `onStateChanged`을 클릭하고 초기화된 오류 및 오류를 확인합니다.

1. 미디어 플레이어의 상태가 INITIALIZED로 변경되면 `MediaPlayer.prepareToPlay`

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 호출이 `prepareToPlay` 시작되면 광고 해상도와 배치 프로세스가 시작됩니다.
1. TVSDK가 `onPrepared` 콜백을 호출하면 미디어 스트림이 성공적으로 로드되고 재생될 준비가 됩니다.

   미디어 스트림이 로드되면 가 `MediaPlayerItem` 만들어집니다.
>오류가 발생하면 오류 상태로 `MediaPlayer` 전환됩니다. 또한 `PlaybackEventListener.onStateChanged`콜백을 호출하여 애플리케이션에 알립니다.
>
>이렇게 하면 여러 매개 변수가 전달됩니다.>
>* 값이 `state` 있는 유형의 `MediaPlayer.PlayerState` 매개 변수입니다 `MediaPlayer.PlayerState.ERROR`.
   >
   >
* 오류 이벤트에 대한 진단 정보가 포함된 유형의 `notification` `MediaPlayerNotification` 매개 변수입니다.


다음 간소화된 샘플 코드는 미디어 리소스를 로드하는 프로세스를 보여 줍니다.

>```java>
>// mediaResource is a properly configured MediaResource instance 
>// mediaPlayer is a MediaPlayer instance 
>// register a PlaybackEventListener implementation with the MediaPlayer  
>instancemediaPlayer.addEventListener( 
>   MediaPlayer.Event.PLAYBACK, 
>   new MediaPlayer.PlaybackEventListener()) { 
>       @Overridepublic void onPrepared() { 
>               // at this point, the resource is successfully loaded and available 
>               // and the MediaPlayer is ready to start the playback 
>               // once the resource is loaded, the MediaPlayer is able to 
>               // provide a reference to the current "playable item" 
> 
>        
       MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
> 
>        
       if (playerItem != null) {     
>                       // here we can take a look at the properties of the     
>                       // loaded stream 
>               } 
>       } @Overridepublic void onStateChanged( 
>               MediaPlayer.PlayerState state,  
>               MediaPlayerNotification notification) { 
>               if (state == MediaPlayer.PlayerState.ERROR) { 
>                       // something bad happened - the resource cannot be loaded    
>                       // details about the problem are provided via the  
>                       // MediaPlayerNotification instance 
>               }  
>               elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
>                       mediaPlayer.prepareToPlay(); 
>               } 
>       } 
>       // implementation of the other methods in the PlaybackEventListener interface... 
>} 
>
>
```>


