---
description: 타임라인 업데이트에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.
title: TimelineUpdatedEvent에 대한 리스너 추가
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# TimelineUpdatedEvent에 대한 리스너 추가{#add-listeners-for-timelineupdatedevent}

타임라인 업데이트에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.

타임라인이 업데이트될 때마다 `MediaPlayer` 디스패치 `AdobePSDK.TimelineEvent` 유형 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. 적절한 리스너를 구현합니다.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. 이벤트 리스너를 등록합니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
