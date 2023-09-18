---
description: 이벤트 핸들러를 사용하면 브라우저 TVSDK가 이벤트에 응답할 수 있습니다.
title: 이벤트 리스너 및 콜백 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 이벤트 리스너 및 콜백 구현{#implement-event-listeners-and-callbacks}

이벤트 핸들러를 사용하면 브라우저 TVSDK가 이벤트에 응답할 수 있습니다.

이벤트가 발생하면 브라우저 TVSDK의 이벤트 메커니즘이 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 핸들러로 전달합니다.

애플리케이션에 영향을 주는 브라우저 TVSDK 이벤트에 대해 애플리케이션이 이벤트 리스너를 구현해야 합니다.

1. 애플리케이션이 수신해야 하는 이벤트를 결정합니다.

   * **필수 이벤트**: 모든 재생 이벤트를 수신합니다.

     >[!IMPORTANT]
     >
     >재생 이벤트 `STATUS_CHANGED` 는 오류를 포함하여 플레이어 상태를 제공합니다. 모든 상태가 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**: 애플리케이션에 따라 선택 사항입니다.

     예를 들어 재생에 광고를 통합하는 경우 모두 수신 대기하십시오 `AdBreakPlaybackEvent` 및 `AdPlaybackEvent` 이벤트.

1. 각 이벤트에 대해 이벤트 리스너를 구현합니다.

   브라우저 TVSDK가 이벤트-리스너 콜백에 매개 변수 값을 반환합니다. 이러한 값은 리스너에서 적절한 작업을 수행하는 데 사용할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   예:

   * 이벤트 유형: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 이벤트 속성: `MediaPlayerStatus.<event>` 다음과 같이 사용됨:

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. 콜백 리스너를 `MediaPlayer` 을 사용한 개체 `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
