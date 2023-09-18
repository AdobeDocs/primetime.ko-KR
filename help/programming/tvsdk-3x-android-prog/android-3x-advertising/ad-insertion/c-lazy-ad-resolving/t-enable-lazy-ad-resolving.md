---
description: 기존 지연 광고 로드 메커니즘을 사용하여 지연 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(지연 광고 해결은 기본적으로 비활성화됨).
keywords: 지연;광고 해결 중;광고 로드;지연 로드
title: 지연 광고 해결 활성화
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 지연 광고 해결 활성화 {#enable-lazy-ad-resolving}

기존 지연 광고 로드 메커니즘을 사용하여 지연 광고 해결 기능을 활성화하거나 비활성화할 수 있습니다(지연 광고 해결은 기본적으로 비활성화됨).

를 호출하여 지연 광고 해결을 활성화하거나 비활성화할 수 있습니다. [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) true 또는 false 포함

* 부울 사용 *hasDelayAdLoading* 및 *setDelayAdLoading* 광고 해상도 타이밍과 타임라인에 광고 배치를 제어하기 위한 AdvertisingMetadata의 메서드는 다음과 같습니다.

   * If *hasDelayAdLoading* false를 반환합니다. TVSDK는 모든 광고가 해결되고 준비됨 상태로 전환되기 전에 배치될 때까지 대기합니다.
   * If *hasDelayAdLoading* true를 반환합니다. TVSDK는 초기 광고만 확인하고 준비됨 상태로 전환합니다.

      * 나머지 광고는 재생 중에 해결되고 배치됩니다.

   * *hasPreroll *또는 *hasLivePreroll* false를 반환하면, TVSDK는 프리롤 광고가 없다고 가정하고 컨텐츠 재생을 즉시 시작합니다. 기본값은 true입니다.

**지연 광고 해결과 관련된 API:**

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

스크러빙 막대에 광고를 큐로 정확하게 반영하려면 `TimelineEvent`이벤트를 표시하고 이 이벤트를 수신할 때마다 스크러빙 막대를 다시 그립니다.

VOD 스트림에 대해 지연 광고 해결이 활성화된 경우 모든 광고 브레이크가 타임라인에 배치되지만 대부분의 광고 브레이크는 아직 해결되지 않습니다. 응용 프로그램은 다음을 확인하여 이러한 마커를 그릴지 여부를 결정할 수 있습니다. `TimelineMarker::getDuration()`. 값이 0보다 큰 경우 광고 브레이크 내의 광고가 해결되었습니다.

TVSDK는 광고 브레이크가 해결되었을 때와 플레이어가 준비됨 상태로 전환될 때 이 이벤트를 발송합니다.

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
