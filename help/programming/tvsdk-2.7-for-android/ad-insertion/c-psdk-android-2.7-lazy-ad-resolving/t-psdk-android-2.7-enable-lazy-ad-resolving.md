---
description: 기존 레이지 광고 로딩 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제가 활성화되어 있음).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 기존 레이지 광고 로딩 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제가 활성화되어 있음).
seo-title: 지연 광고 해결
title: 지연 광고 해결
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 지연 광고 해결 {#enable-lazy-ad-resolving}

기존 레이지 광고 로딩 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제가 활성화되어 있음).

또는 를 사용하여 AdvertisingMetadata.setDelayLoading을 호출하여 [레이지 광고 해결을 활성화하거나 비활성화할](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 수 `true` 있습니다 `false`.

1. 에서 부울 `hasDelayAdLoading` 및 `setDelayAdLoading` 메서드를 사용하여 `AdvertisingMetadata` 타임라인에서 광고 해상도의 타이밍과 광고 배치를 제어할 수 있습니다.

   * false `hasDelayAdLoading` 를 반환하면 TVSDK가 모든 광고가 해결되고 PREMITED 상태로 전환될 때까지 기다립니다.
   * true `hasDelayAdLoading` 를 반환하면 TVSDK는 초기 광고 및 전환만 준비된 상태로 해결합니다. 나머지 광고는 재생 중에 해결되고 배치됩니다.
   * TVSDK는 false를 `hasPreroll` `hasLivePreroll` 반환하거나 프리롤 광고가 없다고 가정하고 컨텐츠 재생을 즉시 시작합니다. 이 기본값은 true입니다.

      지연 광고 해상도와 관련된 API:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. 스크러빙 막대에 광고를 큐로 정확하게 반영하려면 이 이벤트를 수신할 때마다 `TimelineEvent` 이벤트를 듣고 스크러빙 막대를 다시 그립니다.

   VOD 스트림에 대해 [레이지 광고 확인]이 활성화되면 플레이어가 준비 상태가 될 때 일부 광고가 타임라인에 배치되지 않으므로 플레이어가 스크러빙 막대를 명시적으로 다시 그려야 합니다.

   TVSDK는 스크러빙 막대를 다시 그려야 하는 횟수를 최소화하기 위해 이 이벤트의 디스패치를 최적화합니다.따라서 타임라인 이벤트 수는 타임라인에 배치할 광고 브레이크 수와 관련이 없습니다. 예를 들어 5개의 광고 중단이 있는 경우 정확하게 5개의 이벤트를 받지 못할 수 있습니다.

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>[레이지 광고 확인] 기능이 활성화되어 있는지 또는 비활성화되어 있는지 확인하려면 으로 `AdvertisingMetadata.hasDelayAdLoading`문의하십시오. 반환 값은 `true` 레이지 광고 해결이 활성화됨을 의미합니다.즉, `false` 기능을 사용할 수 없음을 의미합니다.

