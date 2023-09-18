---
description: TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.
title: 재생 이벤트 순서
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 재생 이벤트 순서{#order-of-playback-events}

TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

다음 예는 재생 이벤트가 포함된 일부 이벤트의 순서를 보여줍니다.

* 다음을 통해 미디어 리소스를 성공적으로 로드한 경우 `MediaPlayer.replaceCurrentResource`, 이벤트 순서는 다음과 같습니다.

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.INITIALIZED`

* 다음을 통해 재생을 준비할 때 `MediaPlayer.prepareToPlay`, 이벤트 순서는 다음과 같습니다.

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 광고가 삽입된 경우
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.PREPARED`

* 라이브/선형 스트림의 경우 재생 창이 진행되고 추가 기회가 해결됨에 따라 재생하는 동안 이벤트 순서는 다음과 같습니다.

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 광고가 삽입된 경우

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

다음 예는 일반적인 이벤트 진행률을 보여 줍니다.

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
