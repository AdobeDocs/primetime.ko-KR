---
description: 응용 프로그램에서 ERROR 상태에 대한 응답으로 오류 처리를 수행하도록 한 위치를 설정할 수 있습니다.
seo-description: 응용 프로그램에서 ERROR 상태에 대한 응답으로 오류 처리를 수행하도록 한 위치를 설정할 수 있습니다.
seo-title: 오류 처리 설정
title: 오류 처리 설정
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 오류 처리 설정{#set-up-error-handling}

응용 프로그램에서 ERROR 상태에 대한 응답으로 오류 처리를 수행하도록 한 위치를 설정할 수 있습니다.

1. `AdobePSDK.MediaPlayerStatusChangeEvent`에 대한 이벤트 리스너를 추가합니다.

   예:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 이벤트 리스너에서 `event.status`이 `AdobePSDK.MediaPlayerStatus.ERROR`이면 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리된 후 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스를 로드합니다.

       MediaPlayer 개체가 ERROR 상태인 경우 다음 작업 중 하나를 완료해야 이 상태를 종료할 수 있습니다.
   
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

