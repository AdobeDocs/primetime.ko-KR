---
description: 이벤트 핸들러를 사용하면 TVSDK 이벤트에 응답할 수 있습니다.
seo-description: 이벤트 핸들러를 사용하면 TVSDK 이벤트에 응답할 수 있습니다.
seo-title: 이벤트 리스너 및 콜백 구현
title: 이벤트 리스너 및 콜백 구현
uuid: f186b39e-e634-4f64-977d-279147d76c5c
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04

---


# 이벤트 리스너 및 콜백 구현 {#implement-event-listeners-and-callbacks}

이벤트 핸들러를 사용하면 TVSDK 이벤트에 응답할 수 있습니다.

이벤트가 발생하면 TVSDK의 이벤트 메커니즘은 등록된 이벤트 핸들러를 호출하여 이벤트 정보를 전달합니다.

TVSDK는 `MediaPlayer` 인터페이스 내부의 공용 내부 인터페이스로 수신자를 정의합니다.

응용 프로그램은 응용 프로그램에 영향을 주는 모든 TVSDK 이벤트에 대해 이벤트 리스너를 구현해야 합니다.

1. 응용 프로그램이 수신 대기해야 하는 이벤트를 결정합니다.

   * 필수 이벤트:모든 재생 이벤트에 대한 의견 수렴

      >[!IMPORTANT]
      >
      >플레이어 상태가 알아야 하는 방식으로 변경될 때 발생하는 상태 변경 이벤트를 수신합니다. 이 정보에는 플레이어가 다음에 수행할 수 있는 작업에 영향을 줄 수 있는 오류가 포함됩니다.

   * 애플리케이션에 따라 다른 이벤트에 대해서는 Primetime [플레이어 이벤트 요약을](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)참조하십시오.

1. 각 이벤트에 대한 이벤트 리스너를 구현하고 추가합니다.

   대부분의 이벤트의 경우 TVSDK가 이벤트 리스너에 인수를 전달합니다. 이러한 값은 다음에 수행할 작업을 결정하는 데 도움이 되는 이벤트에 대한 정보를 제공합니다. 열거형은 `MediaPlayerEvent` `MediaPlayer` 전달하는 모든 이벤트를 나열합니다. 자세한 내용은 Primetime [플레이어 이벤트 요약을](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)참조하십시오.

   예를 들어, `mPlayer` 의 인스턴스인 경우 이벤트 리스너를 `MediaPlayer`추가하고 구성하는 방법은 다음과 같습니다.

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

## 이벤트 재생 순서 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK 파섹 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

다음 예는 재생 중에 발생하는 일부 이벤트의 순서를 보여줍니다.

미디어 리소스를 성공적으로 로드할 `MediaPlayer.replaceCurrentResource`경우 이벤트 순서는 다음과 같습니다.

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>기본 스레드에서 미디어 리소스를 로드합니다. 백그라운드 스레드에서 미디어 리소스를 로드하는 경우 이 작업 또는 후속 작업에서 `MediaPlayerException`및 종료와 같은 오류가 발생할 수 있습니다.

재생을 준비하는 `MediaPlayer.prepareToPlay`경우 이벤트의 순서는 다음과 같습니다.

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 광고가 삽입된 경우입니다.
1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARED`

라이브/선형 스트림의 경우 재생 창이 계속 이동하고 추가 기회가 해결되면 재생 중에 이벤트 순서는 다음과 같습니다.

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 광고가 삽입된 경우

## 광고 이벤트 순서 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

재생에 광고가 포함되는 경우 TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스 내의 이벤트에 따라 동작을 구현할 수 있습니다.

광고 재생 시 이벤트 순서는 다음과 같습니다.

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

광고 중단 내의 모든 광고에 대해 다음 이벤트가 전달됩니다.

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

다음 예는 광고 재생 이벤트의 일반적인 진행 상태를 보여줍니다.

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

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 동작을 구현할 수 있습니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 수신 대기하십시오 `MediaPlayerEvent.DRM_METADATA`. TVSDK는 `DRMManager` 클래스를 통해 추가 DRM 이벤트를 전달합니다.

## 로더 이벤트 순서 {#section_5638F8EDACCE422A9425187484D39DCC}

로더 이벤트가 발생할 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 때 TVSDK가 전달됩니다.