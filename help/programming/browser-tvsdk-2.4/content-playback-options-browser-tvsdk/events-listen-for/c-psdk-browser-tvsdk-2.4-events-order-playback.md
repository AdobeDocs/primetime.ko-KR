---
description: 브라우저 TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.
title: 재생 이벤트 순서
exl-id: fd9dc0d5-0f39-4a6d-9d88-1fd49946fedf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 재생 이벤트 순서{#order-of-playback-events}

브라우저 TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

다음 예는 재생 이벤트가 포함된 일부 이벤트의 순서를 보여줍니다.

* 다음을 통해 미디어 리소스를 성공적으로 로드한 경우 `replaceCurrentResource`, 이벤트 순서는 다음과 같습니다.

   * `AdobePSDK.MediaPlayerStatusChangeEvent` 포함 `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* 다음을 통해 재생을 준비할 때 `MediaPlayer.prepareToPlay`, 이벤트 순서는 다음과 같습니다.

   * `AdobePSDK.MediaPlayerStatusChangeEvent` 포함 `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

다음 예는 일반적인 이벤트 진행률을 보여 줍니다.

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
