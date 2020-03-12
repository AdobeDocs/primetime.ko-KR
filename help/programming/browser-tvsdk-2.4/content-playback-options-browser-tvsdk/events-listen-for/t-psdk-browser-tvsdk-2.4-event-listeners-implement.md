---
description: 이벤트 핸들러를 사용하면 브라우저 TVSDK가 이벤트에 응답할 수 있습니다.
seo-description: 이벤트 핸들러를 사용하면 브라우저 TVSDK가 이벤트에 응답할 수 있습니다.
seo-title: 이벤트 리스너 및 콜백 구현
title: 이벤트 리스너 및 콜백 구현
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 이벤트 리스너 및 콜백 구현{#implement-event-listeners-and-callbacks}

이벤트 핸들러를 사용하면 브라우저 TVSDK가 이벤트에 응답할 수 있습니다.

이벤트가 발생하면 Browser TVSDK의 이벤트 메커니즘은 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 처리기에 전달합니다.

응용 프로그램은 응용 프로그램에 영향을 주는 브라우저 TVSDK 이벤트에 대한 이벤트 리스너를 구현해야 합니다.

1. 응용 프로그램이 수신 대기해야 하는 이벤트를 결정합니다.

   * **필수 이벤트**:모든 재생 이벤트에 대한 의견 수렴

      >[!IMPORTANT]
      >
      >재생 이벤트는 오류를 포함하여 플레이어 상태를 `STATUS_CHANGED` 제공합니다. 모든 주가 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**:애플리케이션에 따라 선택 사항입니다.

      예를 들어 재생에 광고를 포함시키는 경우 모든 `AdBreakPlaybackEvent` 이벤트와 `AdPlaybackEvent` 이벤트를 수신합니다.

1. 각 이벤트에 대한 이벤트 리스너를 구현합니다.

   Browser TVSDK는 매개 변수 값을 이벤트 리스너 콜백으로 반환합니다. 이러한 값은 리스너에서 적절한 작업을 수행하기 위해 사용할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   예:

   * 이벤트 유형: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 이벤트 속성:다음과 같이 사용됩니다. `MediaPlayerStatus.<event>`

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

1. 를 사용하여 콜백 리스너를 `MediaPlayer` 개체에 등록합니다 `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
