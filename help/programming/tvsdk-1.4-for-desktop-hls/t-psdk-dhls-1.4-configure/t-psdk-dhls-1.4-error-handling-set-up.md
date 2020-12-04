---
description: 한 곳에서 오류를 처리할 수 있습니다.
seo-description: 한 곳에서 오류를 처리할 수 있습니다.
seo-title: 오류 처리 설정
title: 오류 처리 설정
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 오류 처리 설정{#set-up-error-handling}

한 곳에서 오류를 처리할 수 있습니다.

1. `MediaPlayerStatusChangeEvent.STATUS_CHANGED`에 대한 이벤트 콜백 함수를 구현합니다.

   TVSDK는 `MediaPlayerStatusChangeEvent` 개체와 같은 이벤트 정보를 전달합니다.
1. 콜백에서 이벤트 매개 변수의 상태가 `MediaPlayerStatus.ERROR`이면 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리된 후 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스를 로드합니다.

   `MediaPlayer` 개체가 ERROR 상태에 있는 경우 `MediaPlayer` 개체(`MediaPlayer.reset` 메서드를 통해)를 재설정하거나 새 미디어 리소스( `MediaPlayer.replaceCurrentItem`)를 로드할 때까지 이 상태를 종료할 수 없습니다.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

예:

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```

