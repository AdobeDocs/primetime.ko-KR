---
description: 응용 프로그램에서 ERROR 상태에 대한 응답으로 오류 처리를 수행할 위치를 설정할 수 있습니다.
title: 오류 처리 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 오류 처리 설정{#set-up-error-handling}

응용 프로그램에서 ERROR 상태에 대한 응답으로 오류 처리를 수행할 위치를 설정할 수 있습니다.

1. 에 대한 이벤트 리스너 추가 `AdobePSDK.MediaPlayerStatusChangeEvent`.

   예:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 이벤트 리스너에서 `event.status` 은(는) `AdobePSDK.MediaPlayerStatus.ERROR`를 통해 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리되면 을(를) 재설정합니다. `MediaPlayer` 새 미디어 리소스를 가져오거나 로드합니다.

       MediaPlayer 개체가 ERROR 상태인 경우 다음 작업 중 하나를 완료할 때까지 이 상태를 종료할 수 없습니다.
   
   * 를 사용하여 MediaPlayer 개체 재설정 `MediaPlayer.reset` 메서드를 사용합니다.
   * 다음을 사용하여 새 미디어 리소스 로드 `MediaPlayer.replaceCurrentResource` 메서드를 사용합니다.

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
