---
description: 타임라인 업데이트에 대한 알림을 받으려면 해당 이벤트 리스너를 등록합니다.
seo-description: 타임라인 업데이트에 대한 알림을 받으려면 해당 이벤트 리스너를 등록합니다.
seo-title: TimelineUpdatedEvent용 리스너 추가
title: TimelineUpdatedEvent용 리스너 추가
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# TimelineUpdatedEvent용 리스너 추가{#add-listeners-for-timelineupdatedevent}

타임라인 업데이트에 대한 알림을 받으려면 해당 이벤트 리스너를 등록합니다.

타임라인이 업데이트될 때마다 `MediaPlayer` 디스패치는 `AdobePSDK.TimelineEvent` 유형으로 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`전달됩니다.
1. 적절한 수신기를 구현합니다.

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

