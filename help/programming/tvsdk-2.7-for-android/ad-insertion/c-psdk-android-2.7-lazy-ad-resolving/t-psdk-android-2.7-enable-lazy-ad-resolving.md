---
description: 기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 활성화되어 있음).
keywords: 레이지;광고 확인;광고 로드;delayLoading
title: 게으른 광고 해결
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 지연 광고 해결 활성화 {#enable-lazy-ad-resolving}

기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 활성화되어 있음).

`true` 또는 `false`으로 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)을(를) 호출하여 레이지 광고 해결을 활성화하거나 비활성화할 수 있습니다.

1. `AdvertisingMetadata`의 부울 `hasDelayAdLoading` 및 `setDelayAdLoading` 메서드를 사용하여 타임라인에서 광고 해상도의 시간 및 배치를 제어합니다.

   * `hasDelayAdLoading`이 false를 반환하는 경우 TVSDK는 PREMITED 상태로 전환하기 전에 모든 광고가 해결되고 배치될 때까지 기다립니다.
   * `hasDelayAdLoading`이 true를 반환하면 TVSDK는 초기 광고 및 전환만 PREMITED 상태로 해결합니다. 나머지 광고는 재생 중에 확인되고 배치됩니다.
   * `hasPreroll` 또는 `hasLivePreroll`이 false를 반환하면 TVSDK는 프리롤 광고가 없다고 가정하고 컨텐츠 재생을 즉시 시작합니다. 이 기본값은 true입니다.

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

1. 광고를 스크러빙 막대에 큐로 정확하게 반영하려면 `TimelineEvent` 이벤트를 수신하고 이 이벤트를 수신할 때마다 스크러빙 막대를 다시 그립니다.

   VOD 스트림에 대해 [지연 광고 해결]이 활성화되면 플레이어가 준비 상태(PREPARED 상태)를 입력할 때 일부 광고가 타임라인에 배치되지 않으므로 플레이어가 스크러빙 막대를 명시적으로 다시 그려야 합니다.

   TVSDK는 스크러빙 막대를 다시 그려야 하는 횟수를 최소화하기 위해 이 이벤트의 배치를 최적화합니다.따라서 타임라인 이벤트 수는 타임라인에 배치할 광고 중단 수와 관련이 없습니다. 예를 들어 5개의 광고 할당이 있는 경우 정확하게 5개의 이벤트를 받지 못할 수 있습니다.

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

>레이지 광고 확인 기능이 활성화되어 있는지 아니면 비활성화되어 있는지 확인하려면 `AdvertisingMetadata.hasDelayAdLoading`으로 전화하십시오. `true`의 반환 값은 지연 광고 해제가 활성화되어 있음을 의미합니다.`false`은 기능이 비활성화되었음을 의미합니다.

