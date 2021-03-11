---
description: 한 곳에서 오류를 처리할 수 있습니다.
title: 오류 처리 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# 오류 처리 설정{#set-up-error-handling}

한 곳에서 오류를 처리할 수 있습니다.

1. `MediaPlayerStatusChangeEvent.STATUS_CHANGED`에 대한 이벤트 콜백 함수를 구현합니다.

   TVSDK는 `MediaPlayerStatusChangeEvent` 개체와 같은 이벤트 정보를 전달합니다.
1. 콜백에서 이벤트 매개 변수의 상태가 `MediaPlayerStatus.ERROR`이면 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리된 후 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스를 로드합니다.

   `MediaPlayer` 객체가 ERROR 상태인 경우 `MediaPlayer.reset` 메서드를 통해 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스( `MediaPlayer.replaceCurrentItem`)를 로드해야 이 상태를 종료할 수 있습니다.

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

