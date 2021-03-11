---
description: 이벤트 핸들러를 통해 TVSDK가 이벤트에 응답할 수 있습니다.
title: 이벤트 리스너 및 콜백 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# 이벤트 리스너 및 콜백 구현{#implement-event-listeners-and-callbacks}

이벤트 핸들러를 통해 TVSDK가 이벤트에 응답할 수 있습니다.

이벤트가 발생하면 TVSDK의 이벤트 메커니즘은 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 핸들러에 전달합니다.

TVSDK는 `MediaPlayer` 인터페이스에서 수신기를 공용 내부 인터페이스로 정의합니다.

응용 프로그램은 응용 프로그램에 영향을 주는 TVSDK 이벤트에 대한 이벤트 리스너를 구현해야 합니다.

비디오 분석에 대한 이벤트의 전체 목록은 코어 비디오 재생 추적을 참조하십시오.

1. 응용 프로그램에서 수신해야 하는 이벤트를 결정합니다.

   * **필요한 이벤트**:모든 재생 이벤트에 대한 의견 수렴

      >[!IMPORTANT]
      >
      >재생 이벤트 `onStateChanged`는 오류를 포함하여 플레이어 상태를 제공합니다. 모든 상태가 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**:애플리케이션에 따라 선택 사항입니다.

      예를 들어 재생에 광고를 통합하는 경우 AdPlaybackEventListener 콜백을 구현합니다.

1. 각 이벤트에 대한 이벤트 리스너를 구현합니다.

   TVSDK는 이벤트 리스너 콜백에 매개 변수 값을 반환합니다. 이러한 값은 리스너에서 적절한 작업을 수행하는 데 사용할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   `MediaPlayer.EventListener` 모든 콜백 인터페이스를 나열합니다. 각 인터페이스에는 각 이벤트에 대해 반환되는 콜백 이름과 매개 변수가 표시됩니다.

   예:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. `MediaPlayer.addEventListener`을 사용하여 콜백 리스너를 `MediaPlayer` 개체에 등록합니다.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## 재생 이벤트 순서 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK는 일반적으로 예상 시퀀스로 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

다음 예제에서는 재생 이벤트를 포함하는 일부 이벤트의 순서를 보여 줍니다.

* `MediaPlayer.replaceCurrentResource`을(를) 통해 미디어 리소스를 성공적으로 로드할 때 이벤트의 순서는 다음과 같습니다.

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 상태  `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 상태  `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>기본 스레드에 미디어 리소스를 로드합니다. 배경 스레드에 미디어 리소스를 로드하는 경우 이 작업 또는 후속 TVSDK 작업 또는 둘 다에 오류가 발생할 수 있습니다(예: `IllegalStateException`).

* `MediaPlayer.prepareToPlay`을 통해 재생을 준비할 때 이벤트의 순서는 다음과 같습니다.

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 상태  `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 광고가 삽입된 경우입니다.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 상태  `MediaPlayerStatus.PREPARED`

* 라이브/선형 스트림의 경우 재생 창이 이동하고 추가 기회가 해결되면 재생되는 동안 이벤트의 순서는 다음과 같습니다.

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 광고가 삽입된 경우
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 광고가 삽입된 경우

다음 예는 일반적인 이벤트 진행 상태를 보여줍니다.

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## 광고 이벤트 순서 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

재생에 광고가 포함되면 TVSDK는 일반적으로 예상 시퀀스에 이벤트/알림을 전달합니다. 플레이어는 예상 시퀀스의 이벤트를 기반으로 동작을 구현할 수 있습니다.

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdPlaybackEventListener.onAdBreakStart`
* 광고 노출의 모든 광고에 대해 다음 사항이 전달됩니다.

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (광고를 재생하는 동안 여러 번)
   * `AdPlaybackEventListener.onAdClick` (각 클릭에 대해)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

다음 예는 광고 재생 이벤트의 일반적인 진행 상태를 보여줍니다.

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

광고를 재생할 때 이벤트의 순서는 다음과 같습니다.

* `AdPlaybackEventListener.onAdBreakStart`
* 광고 노출의 모든 광고에 대해 다음 사항이 전달됩니다.

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (광고를 재생하는 동안 여러 번)
   * `AdPlaybackEventListener.onAdClick` (각 클릭에 대해)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

다음 예는 광고 재생 이벤트의 일반적인 진행 상태를 보여줍니다.

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## QoS 이벤트 {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.

다음 예는 이러한 이벤트의 일반적인 진행 상태를 보여줍니다.

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## DRM 이벤트 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 디지털 저작권 관리(DRM) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 응답하여 작업을 구현할 수 있습니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`을 수신하십시오. TVSDK는 `DRMManager` 클래스를 통해 추가 DRM 이벤트를 전달합니다.

다음 예는 일반적인 진행 상태를 보여줍니다.

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 로더 이벤트 {#section_5638F8EDACCE422A9425187484D39DCC}

플레이어는 다음 이벤트를 기반으로 작업을 구현할 수 있습니다.

| 이벤트 | 의미 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 미디어 리소스 로드가 완료되었습니다. |
| `onError` | 미디어 리소스를 로드하는 동안 문제가 발생했습니다. |

