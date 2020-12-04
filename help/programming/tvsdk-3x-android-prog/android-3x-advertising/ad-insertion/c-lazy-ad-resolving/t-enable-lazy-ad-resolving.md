---
description: 기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 비활성화됨).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 비활성화됨).
seo-title: 지연 및 해결
title: 지연 및 해결
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# 지연 및 해결 {#enable-lazy-ad-resolving} 활성화

기존 레이지 광고 로드 메커니즘을 사용하여 레이지 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(기본적으로 레이지 광고 해제는 비활성화됨).

True 또는 false로 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)을 호출하여 레이지 광고 해결을 활성화하거나 비활성화할 수 있습니다.

* AdvertisingMetadata에서 부울 *hasDelayAdLoading* 및 *setDelayAdLoading* 메서드를 사용하여 광고 해상도의 시간 및 타임라인에 광고 배치를 제어합니다.

   * *hasDelayAdLoading*&#x200B;이 false를 반환하는 경우 TVSDK는 모든 광고가 해결되고 PREMITED 상태로 전환되기 전에 대기 중입니다.
   * *hasDelayAdLoading*&#x200B;이 true를 반환하면 TVSDK는 초기 광고 및 전환만 PREMITED 상태로 확인합니다.

      * 나머지 광고는 재생 중에 확인되고 배치됩니다.
   * *hasPreroll *또는 *hasLivePreroll*&#x200B;이 false를 반환하는 경우 TVSDK는 프리롤 광고가 없다고 가정하고 컨텐츠 재생을 즉시 시작합니다. 기본값인 true로 설정됩니다.


**지연 광고 해상도와 관련된 API:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

광고를 스크러빙 막대에 신호로 정확하게 반영하려면 `TimelineEvent`이벤트를 수신하고 이 이벤트를 수신할 때마다 스크럽 막대를 다시 그립니다.

VOD 스트림에 대해 [지연 광고 해결]이 활성화되면 모든 광고 할당이 타임라인에 배치되지만, 많은 광고 할당이 아직 해결되지 않습니다. 애플리케이션에서 `TimelineMarker::getDuration()`을 선택하여 이러한 마커를 표시할지 여부를 결정할 수 있습니다. 값이 0보다 큰 경우 광고 중단 내의 광고가 해결되었습니다.

TVSDK는 광고 중단이 해결되면 이 이벤트를 전달하고, 플레이어가 준비된 상태로 전환될 때도 이 이벤트를 전달합니다.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
