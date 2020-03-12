---
description: 비디오 컨텐츠를 재생할 때 캡션을 표시할 수 있습니다.
seo-description: 비디오 컨텐츠를 재생할 때 캡션을 표시할 수 있습니다.
seo-title: 캡션
title: 캡션
uuid: 4dedcedc-50e5-4983-bb09-3f316337117e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 캡션{#captions}

비디오 컨텐츠를 재생할 때 캡션을 표시할 수 있습니다.

캡션을 처리하려면 `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` 이벤트 리스너를 추가해야 합니다.

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<ph>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</ph>
```

UI 프레임워크는 수정할 수 있는 기본 캡션 동작 구현을 제공합니다. 자막 비헤이비어는 기본 자막 비헤이비어를 확장하여 수정할 수도 있습니다. 예:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer(‘.videoDiv', { 
player:{ 
    mediaResource: 'Specify Resource URL', 
    ccStyle: { 
    font:AdobePSDK.TextFormat.CURSIVE, 
    fontColor:AdobePSDK.TextFormat.BRIGHT_WHITE, 
    edgeColor:AdobePSDK.TextFormat.BLUE, 
    backgroundColor:AdobePSDK.TextFormat.BLACK, 
    fillColor:AdobePSDK.TextFormat.BLUE, 
    size:AdobePSDK.TextFormat.MEDIUM, 
    fontOpacity:100, 
    backgroundOpacity:1, 
    fillOpacity:1 
   } 
 } 
 
}); 
```

