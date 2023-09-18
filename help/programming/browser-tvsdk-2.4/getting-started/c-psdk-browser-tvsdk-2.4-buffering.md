---
description: 콘텐츠가 버퍼링되고 있음을 사용자에게 알리도록 비주얼을 구성할 수 있습니다.
title: 버퍼링
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# 버퍼링{#buffering}

콘텐츠가 버퍼링되고 있음을 사용자에게 알리도록 비주얼을 구성할 수 있습니다.

잘 들어 `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` 및 `AdobePSDK.PSDKEventType.BUFFERING_END` 이벤트. 예:

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

UI 프레임워크는 다음과 같이 확장할 수 있는 기본 버퍼링 오버레이 비헤이비어 구현을 제공합니다.

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

DOM의 결과는 다음과 같습니다.

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```
