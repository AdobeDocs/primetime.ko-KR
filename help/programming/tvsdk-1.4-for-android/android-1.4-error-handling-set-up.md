---
description: 한 곳에서 오류를 처리할 수 있습니다.
seo-description: 한 곳에서 오류를 처리할 수 있습니다.
seo-title: 오류 처리 설정
title: 오류 처리 설정
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# 오류 처리 설정{#set-up-error-handling}

한 곳에서 오류를 처리할 수 있습니다.

1. `MediaPlayerEvent.STATUS_CHANGED`에 대한 이벤트 콜백 함수를 구현합니다.

   TVSDK는 `MediaPlayerStatusChangeEvent` 개체와 같은 이벤트 정보를 전달합니다.
1. 콜백에서 반환된 상태가 `MediaPlayerState.ERROR`이면 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리된 후 `MediaPlayer` 개체를 재설정하거나 새 미디어 리소스를 로드합니다.

   `MediaPlayer` 개체가 오류 상태에 있으면 `MediaPlayer.reset` 메서드를 사용하여 재설정할 때까지 해당 상태로 유지됩니다.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

예:

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```

