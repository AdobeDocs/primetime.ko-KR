---
description: 이벤트 핸들러를 사용하면 TVSDK 이벤트에 응답할 수 있습니다.
title: 이벤트 리스너 및 콜백 구현
exl-id: 1f7977e3-4f96-4c0d-ae33-319c84a33ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 이벤트 리스너 및 콜백 구현  {#implement-event-listeners-and-callbacks}

이벤트 핸들러를 사용하면 TVSDK 이벤트에 응답할 수 있습니다.

이벤트가 발생하면 TVSDK의 이벤트 메커니즘이 등록된 이벤트 핸들러를 호출하여 이벤트 정보를 전달합니다.

TVSDK는 리스너를 내부 공용 내부 인터페이스로 정의합니다 `MediaPlayer` 인터페이스.

애플리케이션에 영향을 주는 모든 TVSDK 이벤트에 대해 애플리케이션이 이벤트 리스너를 구현해야 합니다.

1. 애플리케이션이 수신해야 하는 이벤트를 결정합니다.

   * 필수 이벤트: 모든 재생 이벤트를 수신합니다.

      >[!IMPORTANT]
      >
      >플레이어의 상태가 알아야 하는 방식으로 변경될 때 발생하는 상태 변경 이벤트를 수신합니다. 이 태그가 제공하는 정보에는 플레이어가 다음에 수행할 수 있는 작업에 영향을 줄 수 있는 오류가 포함되어 있습니다.

   * 다른 이벤트의 경우 애플리케이션에 따라 다음을 참조하십시오.  [Primetime 플레이어 이벤트 요약](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. 각 이벤트에 대한 이벤트 리스너를 구현하고 추가합니다.

   대부분의 이벤트에 대해 TVSDK는 인수를 이벤트 리스너에 전달합니다. 이러한 값은 다음에 수행할 작업을 결정하는 데 도움이 되는 이벤트에 대한 정보를 제공합니다. 다음 `MediaPlayerEvent` 열거형에는 `MediaPlayer` 디스패치. 자세한 내용은  [Primetime 플레이어 이벤트 요약](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   예를 들어 다음과 같습니다. `mPlayer` 의 인스턴스임 `MediaPlayer`: 이벤트 리스너를 추가하고 구성하는 방법은 다음과 같습니다.

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## 재생 이벤트 순서 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상되는 시퀀스의 이벤트를 기반으로 작업을 구현할 수 있습니다.

다음 예는 재생 중에 발생하는 일부 이벤트의 순서를 보여줍니다.

다음을 통해 미디어 리소스를 성공적으로 로드한 경우 `MediaPlayer.replaceCurrentResource`, 이벤트 순서는 다음과 같습니다.

1. `MediaPlayerEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>기본 스레드에서 미디어 리소스를 로드합니다. 백그라운드 스레드에 미디어 리소스를 로드하는 경우 이 작업 또는 후속 작업에서 오류가 발생할 수 있습니다. `MediaPlayerException`및 를 종료하십시오.

다음을 통해 재생을 준비할 때 `MediaPlayer.prepareToPlay`, 이벤트 순서는 다음과 같습니다.

1. `MediaPlayerEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 광고를 삽입한 경우.
1. `MediaPlayerEvent.STATUS_CHANGED` (상태) `MediaPlayerStatus.PREPARED`

라이브/선형 스트림의 경우 재생 창이 진행되고 추가 기회가 해결됨에 따라 재생하는 동안 이벤트 순서는 다음과 같습니다.

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 광고가 삽입된 경우

## 광고 이벤트 순서 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

재생에 광고가 포함되는 경우 TVSDK는 일반적으로 예상되는 시퀀스로 이벤트/알림을 발송합니다. 플레이어는 예상 시퀀스 내의 이벤트를 기반으로 작업을 구현할 수 있습니다.

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

광고 브레이크 내의 모든 광고에 대해 다음 이벤트가 발송됩니다.

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

다음 예는 광고 재생 이벤트의 일반적인 진행률을 보여 줍니다.

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## DRM 이벤트 순서 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 작업을 구현할 수 있습니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 다음을 들어보십시오. `MediaPlayerEvent.DRM_METADATA`. TVSDK는 를 통해 추가 DRM 이벤트를 전달합니다. `DRMManager` 클래스.

## 로더 이벤트 순서 {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK 디스패치 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 로더 이벤트가 발생하는 경우
