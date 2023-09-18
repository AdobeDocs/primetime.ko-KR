---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
title: MediaPlayer에서 미디어 리소스 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# MediaPlayer에서 미디어 리소스 로드 {#load-a-media-resource-in-the-mediaplayer}

MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.

1. MediaPlayer의 재생 가능한 항목을 재생할 새 리소스로 설정합니다.

   를 호출하여 기존 MediaPlayer의 현재 재생 가능한 항목을 바꿉니다. `MediaPlayer.replaceCurrentItem` 기존 항목 전달 `MediaResource` 인스턴스.

1. 구현 등록 `MediaPlayer.PlaybackEventListener` 을 사용한 인터페이스 `MediaPlayer` 인스턴스.

   * `onPrepared`
   * `onStateChanged`, 그리고 초기화됨 및 오류 여부를 확인합니다.

1. 미디어 플레이어의 상태가 INITIALIZED로 변경되면 `MediaPlayer.prepareToPlay`

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 호출 중 `prepareToPlay` 광고 해상도 및 배치 프로세스(있는 경우)를 시작합니다.

1. TVSDK가 `onPrepared` 콜백, 미디어 스트림이 성공적으로 로드되었으며 재생할 준비가 되었습니다.

   미디어 스트림이 로드될 때 `MediaPlayerItem` 이(가) 만들어졌습니다.

>오류가 발생하면 `MediaPlayer` 오류 상태로 전환합니다. 또한 를 호출하여 애플리케이션에 알립니다. `PlaybackEventListener.onStateChanged`callback.
>
>이렇게 하면 다음과 같은 여러 매개 변수가 전달됩니다.
>* A `state` 유형의 매개변수 `MediaPlayer.PlayerState` (값: `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` 유형의 매개변수 `MediaPlayerNotification` 오류 이벤트에 대한 진단 정보를 포함합니다.

다음은 미디어 리소스 로드 프로세스를 설명하는 간소화된 샘플 코드입니다.

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
