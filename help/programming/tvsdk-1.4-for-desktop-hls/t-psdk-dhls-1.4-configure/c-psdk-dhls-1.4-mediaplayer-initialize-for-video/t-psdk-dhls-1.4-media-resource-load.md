---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
title: MediaPlayer에서 미디어 리소스 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# MediaPlayer에서 미디어 리소스 로드{#load-a-media-resource-in-the-mediaplayer}

MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 설정 `MediaPlayer` 재생할 새 리소스가 있는 오브젝트의 재생 가능 항목.

   를 호출하여 기존 MediaPlayer의 현재 재생 가능한 항목을 바꿉니다. `MediaPlayer.replaceCurrentResource` 기존 항목 전달 `MediaResource` 인스턴스.

1. 적어도 다음 변경 사항을 확인하십시오.

   * 초기화됨
   * 준비됨
   * 오류

     이러한 이벤트를 통해 `MediaPlayer` 미디어 리소스가 성공적으로 로드되면 개체가 응용 프로그램에 알릴 수 있습니다.

1. 미디어 플레이어의 상태가 INITIALIZED로 변경되면 `MediaPlayer.prepareToPlay`

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 호출 중 `prepareToPlay` 광고 해상도 및 배치 프로세스(있는 경우)를 시작합니다.

1. 미디어 플레이어 상태가 준비됨으로 변경되면 미디어 스트림이 성공적으로 로드되고 재생이 준비됩니다.

   미디어 스트림이 로드될 때 `MediaPlayerItem` 이(가) 만들어졌습니다.

오류가 발생하면 MediaPlayer가 ERROR 상태로 전환됩니다. 또한 를 발송하여 애플리케이션에 알립니다. `STATUS_CHANGED` 에 대한 이벤트 `MediaPlayerStatusChangeEvent` callback.

이렇게 하면 다음과 같은 여러 매개 변수가 전달됩니다.
* A `type` 값이 있는 유형 문자열의 매개변수 `ERROR`.

* A `MediaError` 오류 이벤트에 대한 진단 정보가 포함된 알림을 받는 데 사용할 수 있는 매개 변수입니다.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

다음은 미디어 리소스 로드 프로세스를 설명하는 간소화된 샘플 코드입니다.

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
