---
description: 오류를 처리할 하나의 레이스를 설정할 수 있습니다.
title: 오류 처리 설정
exl-id: 594cd9b8-491f-4972-990a-5657f87c7f89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 오류 처리 설정 {#set-up-error-handling}

오류를 처리할 하나의 레이스를 설정할 수 있습니다.

1. 에 대한 이벤트 콜백 함수 구현 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK는 다음과 같은 이벤트 정보를 전달합니다. `MediaPlayerStatusChangeEvent` 개체.
1. 콜백에서 반환된 상태가 다음과 같은 경우 `MediaPlayerStatus.ERROR`모든 오류를 처리할 논리를 제공합니다.
1. 오류가 처리되면 을(를) 재설정합니다. `MediaPlayer` 새 미디어 리소스를 가져오거나 로드합니다.

   다음의 경우 `MediaPlayer` 개체는 오류 상태에 있으며 를 사용하여 재설정할 때까지 해당 상태로 유지됩니다. `MediaPlayer.reset` 메서드를 사용합니다.

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
