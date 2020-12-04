---
description: 콘텐츠가 버퍼링되고 있음을 사용자에게 알리기 위해 시각적 요소를 구성할 수 있습니다.
seo-description: 콘텐츠가 버퍼링되고 있음을 사용자에게 알리기 위해 시각적 요소를 구성할 수 있습니다.
seo-title: 버퍼링
title: 버퍼링
uuid: da9498ee-c736-4093-97a2-250d3ad56d49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 0%

---


# 버퍼링{#buffering}

콘텐츠가 버퍼링되고 있음을 사용자에게 알리기 위해 시각적 요소를 구성할 수 있습니다.

`AdobePSDK.PSDKEventType.BUFFERING_BEGIN` 및 `AdobePSDK.PSDKEventType.BUFFERING_END` 이벤트를 수신합니다. 예:

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

UI 프레임워크는 다음과 같이 확장할 수 있는 기본 버퍼링 오버레이 동작 구현을 제공합니다.

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

다음은 DOM의 결과입니다.

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```

