---
description: 모든 광고를 로드하고 타임라인에 배치하기 전에 재생을 허용할지 여부를 지정할 수 있습니다. 이렇게 재생을 시작하면 뷰어가 기본 컨텐츠에 보다 빠르게 액세스할 수 있습니다. 이 기능은 실시간 DVR에만 적용되며 VOD 자산과 같이 작동하지 않습니다.
title: 레이지 광고 로딩 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 지연 광고 로딩 사용{#enable-lazy-ad-loading}

모든 광고를 로드하고 타임라인에 배치하기 전에 재생을 허용할지 여부를 지정할 수 있습니다. 이렇게 재생을 시작하면 뷰어가 기본 컨텐츠에 보다 빠르게 액세스할 수 있습니다. 이 기능은 실시간 DVR에만 적용되며 VOD 자산과 같이 작동하지 않습니다.

1. `AdvertisingMetadata`에서 부울 속성 `delayAdLoading`을 사용합니다.

   * false인 경우 TVSDK는 PREMITED 상태로 전환하기 전에 모든 광고가 해결되고 배치될 때까지 기다립니다. 기본적으로 false입니다.
   * true인 경우 TVSDK는 초기 광고 및 전환만 준비된 상태로 확인합니다. 나머지 광고는 재생 중에 확인되고 배치됩니다.

1. Adobe Primetime 광고 의사 결정을 사용하여 지연된 광고 로드를 활성화하려면 `AuditudeSettings`을(를) 만들 때 `true`으로 설정합니다.

   `AuditudeSettings` 클래스는 `AdvertisingMetadata`에서 이 속성을 상속하지만 현재 값은 상속하지 않습니다.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 광고를 스크러빙 막대에 큐로 정확하게 반영하려면 `TimelineEvent`에 귀를 기울입니다. `TIMELINE_UPDATED` 이벤트를 생성하고 이 이벤트를 수신할 때마다 스크러빙 막대를 다시 그립니다.

   VoD 스트림에서 지연된 광고 로드를 사용하는 경우 플레이어에서 준비 상태를 입력할 때 일부 광고가 타임라인에 배치되지 않으므로 스크러빙 막대를 명시적으로 다시 그려야 합니다.

   TVSDK는 스크러빙 막대를 다시 그려야 하는 횟수를 최소화하기 위해 이 이벤트의 배치를 최적화합니다.따라서 타임라인 이벤트 수는 타임라인에 배치할 광고 중단 수와 관련이 없습니다. 예를 들어 5개의 광고 할당이 있는 경우 정확하게 5개의 이벤트를 받지 못할 수 있습니다.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

