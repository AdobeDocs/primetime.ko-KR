---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.
seo-title: 미디어 플레이어에서 미디어 리소스 로드
title: 미디어 플레이어에서 미디어 리소스 로드
uuid: 1a27b83b-afa6-48c7-a701-e11b2d280810
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 미디어 플레이어 {#load-a-media-resource-in-the-media-player}에 미디어 리소스 로드

MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다. 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 새 리소스를 재생하도록 미디어 플레이어를 설정합니다.

   `MediaPlayer.replaceCurrentResource()`을(를) 호출하고 기존 `MediaResource` 인스턴스를 전달하여 현재 재생 가능한 항목을 바꿉니다.

   리소스 로드 프로세스가 시작됩니다.

1. `MediaPlayerEvent.STATUS_CHANGED` 이벤트를 `MediaPlayer` 인스턴스로 등록합니다. 콜백에서 다음 상태 값 이상을 확인합니다.

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   이러한 이벤트를 통해, 미디어 리소스를 성공적으로 불러오면 `MediaPlayer` 개체가 응용 프로그램에 알립니다.
1. 미디어 플레이어의 상태가 `INITIALIZED`으로 변경되면 `MediaPlayer.prepareToPlay()`를 호출할 수 있습니다.

   이 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 새 `MediaPlayerItem`이(가) 재생할 준비가 되었습니다. `prepareToPlay()`을(를) 호출하면 광고 해상도 및 배치 프로세스가 시작됩니다.

오류가 발생하면 미디어 플레이어는 `ERROR` 상태로 전환됩니다.

다음 간소화된 샘플 코드는 미디어 리소스를 로드하는 프로세스를 보여 줍니다.

```java>
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```
