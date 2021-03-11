---
description: 타임라인 업데이트에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.
title: TimelineUpdatedEvent용 리스너 추가
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent} 리스너를 추가합니다.

타임라인 업데이트에 대한 알림을 받으려면 적절한 이벤트 리스너를 등록합니다.

타임라인이 업데이트될 때마다 `MediaPlayer`은 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` 유형으로 `AdobePSDK.TimelineEvent`을(를) 전달합니다.
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

