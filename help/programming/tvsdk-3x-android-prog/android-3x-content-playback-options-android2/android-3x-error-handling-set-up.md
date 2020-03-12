---
description: 한 개의 레이스로 오류를 처리할 수 있습니다.
seo-description: 한 개의 레이스로 오류를 처리할 수 있습니다.
seo-title: 오류 처리 설정
title: 오류 처리 설정
uuid: 7c122830-6259-4e95-882e-fb1700454e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 오류 처리 설정 {#set-up-error-handling}

한 개의 레이스로 오류를 처리할 수 있습니다.

1. 에 대한 이벤트 콜백 함수를 `MediaPlayerEvent.STATUS_CHANGED`구현합니다.

   TVSDK는 `MediaPlayerStatusChangeEvent` 개체와 같은 이벤트 정보를 전달합니다.
1. 콜백에서 반환된 상태가 `MediaPlayerStatus.ERROR`인 경우 모든 오류를 처리하는 논리를 제공합니다.
1. 오류가 처리되면 개체를 재설정하거나 새 미디어 리소스를 로드합니다. `MediaPlayer`

   객체가 오류 상태에 `MediaPlayer` 있을 때는 메서드를 사용하여 재설정할 때까지 해당 상태로 유지됩니다 `MediaPlayer.reset` .

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

예:

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```
