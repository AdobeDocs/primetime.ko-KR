---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-title: MediaPlayer에서 미디어 리소스 로드
title: MediaPlayer에서 미디어 리소스 로드
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: 84924d84bfa436a8807c2e8d74d1dc268d457051

---


# MediaPlayer에서 미디어 리소스 로드{#load-a-media-resource-in-the-mediaplayer}

MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 재생할 새 리소스로 `MediaPlayer` 개체의 재생 가능한 항목을 설정합니다.

   기존 인스턴스를 호출하고 전달하여 기존 MediaPlayer의 현재 재생 가능한 항목을 `MediaPlayer.replaceCurrentResource` 교체합니다 `MediaResource` .

1. 다음 변경 사항 이상을 확인하십시오.

   * 초기화됨
   * 준비 완료
   * 오류

      이러한 이벤트를 통해 미디어 리소스가 성공적으로 로드되면 `MediaPlayer` 개체가 응용 프로그램에 알릴 수 있습니다.

1. 미디어 플레이어의 상태가 INITIALIZED로 변경되면 `MediaPlayer.prepareToPlay`

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 호출이 `prepareToPlay` 시작되면 광고 해상도와 배치 프로세스가 시작됩니다.

1. 미디어 플레이어 상태가 PREPARED로 변경되면 미디어 스트림이 성공적으로 로드되어 재생될 준비가 됩니다.

   미디어 스트림이 로드되면 가 `MediaPlayerItem` 만들어집니다.

오류가 발생하면 MediaPlayer는 ERROR 상태로 전환됩니다. 또한 이벤트를 콜백에 전달하여 응용 프로그램에 알립니다. `STATUS_CHANGED` `MediaPlayerStatusChangeEvent`

이렇게 하면 여러 매개 변수가 전달됩니다.
* 값이 있는 문자열 유형의 `type` 매개 변수입니다 `ERROR`.

* 오류 이벤트에 대한 진단 정보가 포함된 알림을 얻는 데 사용할 수 있는 `MediaError` 매개 변수입니다.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

다음 간소화된 샘플 코드는 미디어 리소스를 로드하는 프로세스를 보여 줍니다.

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
