---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.
title: 미디어 플레이어에서 미디어 리소스 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 미디어 플레이어에서 미디어 리소스 로드 {#load-a-media-resource-in-the-media-player}

MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다. 이는 미디어 리소스를 로드하는 한 가지 방법입니다.

1. 미디어 플레이어를 설정하여 새 리소스를 재생합니다.

   를 호출하여 현재 재생 가능한 항목 바꾸기 `MediaPlayer.replaceCurrentResource()` 기존 항목 전달 `MediaResource` 인스턴스.

   리소스 로드 프로세스가 시작됩니다.

1. 등록 `MediaPlayerEvent.STATUS_CHANGED` 이 포함된 이벤트 `MediaPlayer` 인스턴스. 콜백에서 최소한 다음 상태 값이 있는지 확인하십시오.

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   이러한 이벤트를 통해 `MediaPlayer` 개체가 미디어 리소스를 성공적으로 로드하면 애플리케이션에 알립니다.
1. 미디어 플레이어의 상태가 (으)로 변경되는 경우 `INITIALIZED`, 를 호출할 수 있습니다. `MediaPlayer.prepareToPlay()`.

   이 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 새로운 `MediaPlayerItem` 을(를) 재생할 준비가 되었습니다. 호출 중 `prepareToPlay()` 광고 해상도 및 배치 프로세스(있는 경우)를 시작합니다.

오류가 발생하면 미디어 플레이어에서 `ERROR` 상태.

다음은 미디어 리소스 로드 프로세스를 설명하는 간소화된 샘플 코드입니다.

```java
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
