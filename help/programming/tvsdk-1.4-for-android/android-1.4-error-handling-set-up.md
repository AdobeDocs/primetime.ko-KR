---
description: 오류를 처리할 단일 위치를 설정합니다.
title: 오류 처리 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 오류 처리 설정{#set-up-error-handling}

오류를 처리할 단일 위치를 설정합니다.

1. 에 대한 이벤트 콜백 함수 구현 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK는 다음과 같은 이벤트 정보를 전달합니다. `MediaPlayerStatusChangeEvent` 개체.
1. 콜백에서 반환된 상태가 다음과 같은 경우 `MediaPlayerState.ERROR`모든 오류를 처리할 논리를 제공합니다.
1. 오류가 처리되면 을(를) 재설정합니다. `MediaPlayer` 새 미디어 리소스를 가져오거나 로드합니다.

   다음의 경우 `MediaPlayer` 개체가 오류 상태에 있으므로 를 사용하여 재설정할 때까지 해당 상태로 유지됩니다. `MediaPlayer.reset` 메서드를 사용합니다.

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
