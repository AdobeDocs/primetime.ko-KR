---
description: 오류를 처리할 단일 위치를 설정합니다.
title: 오류 처리 설정
exl-id: ce4a2954-0166-43af-afdf-0aa24659f1ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 오류 처리 설정{#set-up-error-handling}

오류를 처리할 단일 위치를 설정합니다.

1. 에 대한 이벤트 콜백 함수 구현 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK는 다음과 같은 이벤트 정보를 전달합니다. `MediaPlayerStatusChangeEvent` 개체.
1. 콜백에서 이벤트 매개 변수의 상태가 인 경우 `MediaPlayerStatus.ERROR`모든 오류를 처리할 논리를 제공합니다.
1. 오류가 처리되면 을(를) 재설정합니다. `MediaPlayer` 새 미디어 리소스를 가져오거나 로드합니다.

   다음의 경우 `MediaPlayer` 개체가 ERROR 상태이므로 재설정할 때까지 이 상태를 종료할 수 없습니다. `MediaPlayer` 개체(를 통해) `MediaPlayer.reset` 메서드) 또는 새 미디어 리소스 로드( `MediaPlayer.replaceCurrentItem`).

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
