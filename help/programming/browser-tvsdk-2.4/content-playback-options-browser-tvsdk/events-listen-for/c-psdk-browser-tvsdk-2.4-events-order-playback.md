---
description: 브라우저 TVSDK는 일반적으로 예상 시퀀스로 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-description: 브라우저 TVSDK는 일반적으로 예상 시퀀스로 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-title: 재생 이벤트 순서
title: 재생 이벤트 순서
uuid: 259a9a2d-3d28-4240-b392-cc81f5c3f0cf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 재생 이벤트 순서{#order-of-playback-events}

브라우저 TVSDK는 일반적으로 예상 시퀀스로 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

다음 예는 재생 이벤트를 포함하는 일부 이벤트의 순서를 보여줍니다.

* `replaceCurrentResource`을(를) 통해 미디어 리소스를 성공적으로 로드할 경우 이벤트의 순서는 다음과 같습니다.

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with  `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* `MediaPlayer.prepareToPlay`을 통해 재생을 준비하는 경우 이벤트의 순서는 다음과 같습니다.

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with  `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

다음 예제는 이벤트의 일반적인 진행 상태를 보여줍니다.

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```

