---
description: 기존 지연 광고 로드 메커니즘을 사용하여 지연 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(지연 광고 해결은 기본적으로 활성화되어 있음).
keywords: 지연;광고 해결 중;광고 로드;지연 로드
title: 지연 광고 해결 활성화
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 지연 광고 해결 활성화 {#enable-lazy-ad-resolving}

기존 지연 광고 로드 메커니즘을 사용하여 지연 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(지연 광고 해결은 기본적으로 활성화되어 있음).

를 호출하여 지연 광고 해결을 활성화하거나 비활성화할 수 있습니다. [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 포함 `true` 또는 `false`.

1. 부울 사용 `hasDelayAdLoading` 및 `setDelayAdLoading` 의 메서드 `AdvertisingMetadata` 광고 해상도 타이밍과 타임라인에 광고 배치를 제어하려면 다음을 수행하십시오.

   * If `hasDelayAdLoading` false를 반환합니다. TVSDK는 모든 광고가 해결되고 준비됨 상태로 전환되기 전에 배치될 때까지 대기합니다.
   * If `hasDelayAdLoading` true를 반환합니다. TVSDK는 초기 광고만 확인하고 준비됨 상태로 전환합니다. 나머지 광고는 재생 중에 해결되고 배치됩니다.
   * 날짜 `hasPreroll` 또는 `hasLivePreroll` false를 반환하면, TVSDK는 프리롤 광고가 없다고 가정하고 컨텐츠 재생을 즉시 시작합니다. 기본값은 true입니다.

     지연 광고 해결과 관련된 API:

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

1. 스크러빙 막대에 광고를 큐로 정확하게 반영하려면 `TimelineEvent` 이벤트를 표시하고 이 이벤트를 수신할 때마다 스크러빙 막대를 다시 그립니다.

   VOD 스트림에 대해 레이지 광고 해결 이 활성화된 경우 플레이어가 PREPARED 상태에 들어와도 타임라인에 모든 광고가 배치되는 것은 아니므로 플레이어가 스크러빙 막대를 명시적으로 다시 그려야 합니다.

   TVSDK는 스크러빙 막대를 다시 그려야 하는 횟수를 최소화하도록 이 이벤트의 발송을 최적화합니다. 따라서 타임라인 이벤트 수는 타임라인에 배치할 광고 브레이크 수와 관련이 없습니다. 예를 들어 5개의 광고 브레이크가 있는 경우 정확히 5개의 이벤트를 받지 못할 수 있습니다.

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

>지연 광고 해결 기능이 활성화되었는지 여부를 확인하려면 을 호출하십시오. `AdvertisingMetadata.hasDelayAdLoading`. 반환 값: `true` 는 지연 광고 해결이 활성화되었음을 의미합니다. `false` 은(는) 기능이 비활성화되었음을 의미합니다.
