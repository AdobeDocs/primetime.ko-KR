---
description: 모든 광고가 로드되어 타임라인에 배치되기 전에 재생을 허용할지 여부를 지정할 수 있습니다. 이러한 방식으로 재생을 시작하면 뷰어가 기본 콘텐츠에 더 빠르게 액세스할 수 있습니다. 이 기능은 라이브 DVR에만 적용할 수 있으며, VOD 자산과 같이 작동하지는 않습니다.
title: 레이지 광고 로드 활성화
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 레이지 광고 로드 활성화{#enable-lazy-ad-loading}

모든 광고가 로드되어 타임라인에 배치되기 전에 재생을 허용할지 여부를 지정할 수 있습니다. 이러한 방식으로 재생을 시작하면 뷰어가 기본 콘텐츠에 더 빠르게 액세스할 수 있습니다. 이 기능은 라이브 DVR에만 적용할 수 있으며, VOD 자산과 같이 작동하지는 않습니다.

1. 부울 속성 사용 `delayAdLoading` 위치: `AdvertisingMetadata`.

   * false인 경우 TVSDK는 모든 광고가 해결되고 준비됨 상태로 전환되기 전에 배치될 때까지 기다립니다. 기본적으로 false입니다.
   * true인 경우 TVSDK는 초기 광고만 확인하고 준비됨 상태로 전환합니다. 나머지 광고는 재생 중에 해결되고 배치됩니다.

1. 또한 Adobe Primetime 광고 의사 결정을 통해 지연된 광고 로드를 활성화하려면 다음을 설정하십시오. `true` 생성 시 `AuditudeSettings`.

   다음 `AuditudeSettings` 클래스는 다음에서 이 속성을 상속합니다. `AdvertisingMetadata`, 그러나 는 현재 값을 상속하지 않습니다.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 스크러빙 막대에 광고를 큐로 정확하게 반영하려면 `TimelineEvent`. `TIMELINE_UPDATED` 이벤트를 표시하고 이 이벤트를 수신할 때마다 스크러빙 막대를 다시 그립니다.

   VoD 스트림이 지연된 광고 로드를 사용하는 경우 플레이어가 PREPARED 상태에 들어갈 때 모든 광고가 타임라인에 배치되는 것은 아니므로 스크러빙 막대를 명시적으로 다시 그려야 합니다.

   TVSDK는 스크러빙 막대를 다시 그려야 하는 횟수를 최소화하도록 이 이벤트의 발송을 최적화합니다. 따라서 타임라인 이벤트 수는 타임라인에 배치할 광고 브레이크 수와 관련이 없습니다. 예를 들어 5개의 광고 브레이크가 있는 경우 정확히 5개의 이벤트를 받지 못할 수 있습니다.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
