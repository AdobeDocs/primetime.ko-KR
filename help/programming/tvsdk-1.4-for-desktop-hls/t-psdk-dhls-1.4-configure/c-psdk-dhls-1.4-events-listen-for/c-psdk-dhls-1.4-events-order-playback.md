---
description: TVSDK 파섹 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-description: TVSDK 파섹 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.
seo-title: 이벤트 재생 순서
title: 이벤트 재생 순서
uuid: 4a9ea66b-a383-46ff-9ab8-983b1dd7f935
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 이벤트 재생 순서{#order-of-playback-events}

TVSDK 파섹 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

다음 예는 재생 이벤트를 포함하는 일부 이벤트의 순서를 보여줍니다.

* 미디어 리소스를 성공적으로 로드할 `MediaPlayer.replaceCurrentResource`경우 이벤트 순서는 다음과 같습니다.

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZED`

* 재생을 준비하는 `MediaPlayer.prepareToPlay`경우 이벤트의 순서는 다음과 같습니다.

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 광고가 삽입된 경우
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARED`

* 라이브/선형 스트림의 경우 재생 창이 계속 이동하고 추가 기회가 해결되면 재생 중에 이벤트 순서는 다음과 같습니다.

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 광고가 삽입된 경우

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

다음 예는 일반적인 이벤트 진행 상태를 보여줍니다.

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```

