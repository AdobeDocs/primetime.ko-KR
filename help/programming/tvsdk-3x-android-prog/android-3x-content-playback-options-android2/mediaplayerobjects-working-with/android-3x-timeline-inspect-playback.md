---
description: TVSDK에서 재생하는 현재 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 지정 스크러빙 막대 컨트롤을 응용 프로그램에 표시할 때 가장 유용합니다.
title: Inspect 재생 타임라인
exl-id: 95792354-76f6-44fd-9207-73e862b434e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect 재생 타임라인 {#inspect-the-playback-timeline}

TVSDK에서 재생하는 현재 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 지정 스크러빙 막대 컨트롤을 응용 프로그램에 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에서 볼 수 있는 구현 예입니다.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 액세스 권한 `Timeline` 의 개체 `MediaPlayer` 사용 `getTimeline()` 메서드를 사용합니다.

   다음 `Timeline` 클래스는 현재 `MediaPlayer` 인스턴스. 다음 `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 액세스할 수 있도록 합니다. 다음 `Timeline` 클래스는 다음 목록을 통해 반복기를 제공하는 getter 메서드를 제공합니다 `TimelineMarker` 개체.

1. 목록 반복 `TimelineMarkers` 반환된 정보를 사용하여 타임라인을 구현합니다.

       &#39;TimelineMarker&#39; 개체에는 두 가지 정보가 포함됩니다.
   
   * 타임라인에서 마커의 위치(밀리초)
   * 타임라인에서 마커의 지속 시간(밀리초)

1. 다음 내용을 들어 보십시오. `MediaPlayerEvent.TIMELINE_UPDATED` 이벤트 `MediaPlayer` 인스턴스 및 구현 `TimelineUpdatedEventListener.onTimelineUpdated()` 콜백입니다.

   다음 `Timeline` 객체는 `OnTimelineUpdated` 리스너에 대해 설명합니다.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
