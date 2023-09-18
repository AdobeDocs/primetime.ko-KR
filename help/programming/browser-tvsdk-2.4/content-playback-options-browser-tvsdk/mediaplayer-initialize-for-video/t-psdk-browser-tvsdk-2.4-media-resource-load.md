---
description: MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다.
title: MediaPlayer에서 미디어 리소스 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# MediaPlayer에서 미디어 리소스 로드 {#load-a-media-resource-in-the-mediaplayer}

MediaResource를 직접 인스턴스화하고 재생할 비디오 콘텐츠를 로드하여 리소스를 로드합니다.

1. 설정 `MediaPlayer` 재생할 새 리소스가 있는 오브젝트의 재생 가능 항목.

   기존 항목 바꾸기 `MediaPlayer` 를 호출하여 현재 재생 가능한 개체 항목 `replaceCurrentResource` 기존 항목 전달 `MediaResource` 인스턴스.

1. 브라우저 TVSDK가 디스패치될 때까지 대기 `AdobePSDK.MediaPlayerStatusChangeEvent` 포함 `event.status` 이는 다음 중 어느 것과도 같습니다.

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

     이러한 이벤트를 통해 MediaPlayer 개체는 미디어 리소스가 성공적으로 로드되었는지 여부를 응용 프로그램에 알립니다.

1. 미디어 플레이어의 상태가 (으)로 변경되는 경우 `MediaPlayerStatus.INITIALIZED`, 를 호출할 수 있습니다. `MediaPlayer.prepareToPlay`.

   INITIALIZED 상태는 미디어가 성공적으로 로드되었음을 나타냅니다. 호출 중 `prepareToPlay` 광고 해상도 및 배치 프로세스(있는 경우)를 시작합니다.
1. 브라우저 TVSDK가 `MediaPlayerStatus.PREPARED` 이벤트 미디어 스트림이 성공적으로 로드되고(MediaPlayerItem이 만들어짐) 재생이 준비되었습니다.

오류가 발생하면 `MediaPlayer` (으)로 전환 `MediaPlayerStatus.ERROR`.

또한 를 발송하여 애플리케이션에 알립니다. `MediaPlayerStatus.ERROR` 이벤트.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

다음은 미디어 리소스 로드 프로세스를 설명하는 간소화된 샘플 코드입니다.

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
