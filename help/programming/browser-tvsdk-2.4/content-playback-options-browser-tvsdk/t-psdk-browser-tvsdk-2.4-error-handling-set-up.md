---
description: ERROR 상태에 대한 응답으로 오류 처리를 수행하도록 응용 프로그램에서 한 위치를 설정할 수 있습니다.
title: 오류 처리 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 오류 처리 설정{#set-up-error-handling}

ERROR 상태에 대한 응답으로 오류 처리를 수행하도록 응용 프로그램에서 한 위치를 설정할 수 있습니다.

1. `AdobePSDK.MediaPlayerStatusChangeEvent`에 대한 이벤트 리스너를 추가합니다.

   예:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 이벤트 리스너에서 `event.status`이 `AdobePSDK.MediaPlayerStatus.ERROR`이면 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리된 후 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스를 로드합니다.

       MediaPlayer 객체가 ERROR 상태인 경우 다음 작업 중 하나를 완료해야 이 상태를 종료할 수 있습니다.
   
   * `MediaPlayer.reset` 메서드를 사용하여 MediaPlayer 개체를 재설정합니다.
   * `MediaPlayer.replaceCurrentResource` 메서드를 사용하여 새 미디어 리소스를 로드합니다.

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

예:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```

