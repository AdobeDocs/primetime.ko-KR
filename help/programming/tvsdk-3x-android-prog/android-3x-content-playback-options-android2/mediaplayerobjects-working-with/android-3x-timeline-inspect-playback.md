---
description: 현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.
seo-description: 현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.
seo-title: 재생 타임라인 검사
title: 재생 타임라인 검사
uuid: d5d68684-d658-44bc-bfff-952b7946c7fd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 재생 타임라인 검사 {#inspect-the-playback-timeline}

현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에 표시된 구현의 예입니다.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 이 `Timeline` 메서드를 사용하여 에서 개체에 `MediaPlayer` `getTimeline()` 액세스합니다.

   이 `Timeline` 클래스는 인스턴스가 현재 로드한 미디어 항목과 연결된 타임라인의 컨텐츠와 관련된 정보를 캡슐화합니다 `MediaPlayer` . 이 `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 대한 액세스를 제공합니다. 이 `Timeline` 클래스는 `TimelineMarker` 개체 목록을 통해 반복기를 제공하는 getter 메서드를 제공합니다.

1. 목록을 `TimelineMarkers` 반복하고 반환된 정보를 사용하여 타임라인을 구현합니다.

       &#39;TimelineMarker&#39; 개체에는 다음 두 가지 정보가 포함되어 있습니다.
   
   * 타임라인에서 마커의 위치(밀리초 단위)
   * 타임라인에 있는 마커의 지속 시간(밀리초)

1. 인스턴스에서 `MediaPlayerEvent.TIMELINE_UPDATED` 이벤트를 수신하고 `MediaPlayer` 콜백을 구현합니다 `TimelineUpdatedEventListener.onTimelineUpdated()` .

   이 `Timeline` 개체는 `OnTimelineUpdated` 리스너를 호출하여 재생 타임라인에서 발생할 수 있는 변경 사항에 대해 응용 프로그램에 알릴 수 있습니다.

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
