---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다.
seo-description: MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다.
seo-title: MediaPlayer에서 미디어 리소스 로드
title: MediaPlayer에서 미디어 리소스 로드
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# MediaPlayer {#load-a-media-resource-in-the-mediaplayer}에서 미디어 리소스 로드

MediaResource를 직접 인스턴스화하고 재생할 비디오 컨텐츠를 로드하여 리소스를 로드합니다.

1. 재생할 새 리소스로 `MediaPlayer` 개체의 재생 가능한 항목을 설정합니다.

   기존 `MediaPlayer` 개체의 현재 재생 가능한 항목을 `replaceCurrentResource`에 호출하고 기존 `MediaResource` 인스턴스를 전달하여 대체합니다.

1. 다음 중 하나와 동일한 `event.status`로 브라우저 TVSDK가 `AdobePSDK.MediaPlayerStatusChangeEvent`을(를) 전달할 때까지 기다립니다.

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      이러한 이벤트를 통해 MediaPlayer 개체는 미디어 리소스가 성공적으로 로드되었는지 응용 프로그램에 알립니다.

1. 미디어 플레이어의 상태가 `MediaPlayerStatus.INITIALIZED`으로 변경되면 `MediaPlayer.prepareToPlay`를 호출할 수 있습니다.

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. `prepareToPlay`을(를) 호출하면 광고 해상도 및 배치 프로세스가 시작됩니다.
1. Browser TVSDK가 `MediaPlayerStatus.PREPARED` 이벤트를 전달하면 미디어 스트림이 성공적으로 로드되고(MediaPlayerItem이 생성됨) 재생할 수 있습니다.

오류가 발생하면 `MediaPlayer`은 `MediaPlayerStatus.ERROR`으로 전환됩니다.

또한 `MediaPlayerStatus.ERROR` 이벤트를 전달하여 응용 프로그램에 알립니다.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


다음 간소화된 샘플 코드는 미디어 리소스를 로드하는 프로세스를 보여 줍니다.

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
