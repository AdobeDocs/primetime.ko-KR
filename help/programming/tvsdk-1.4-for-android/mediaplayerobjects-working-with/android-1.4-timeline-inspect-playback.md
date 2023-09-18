---
description: TVSDK에서 재생 중인 현재 선택한 항목과 연결된 타임라인에 대한 설명을 가져올 수 있습니다. 이 기능은 응용 프로그램에서 광고 콘텐츠에 해당하는 콘텐츠 섹션이 식별되는 사용자 지정 스크러바 컨트롤을 표시할 때 가장 유용합니다.
title: 재생 타임라인 Inspect
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 재생 타임라인 Inspect{#inspect-the-playback-timeline}

TVSDK에서 재생 중인 현재 선택한 항목과 연결된 타임라인에 대한 설명을 가져올 수 있습니다. 이 기능은 응용 프로그램에서 광고 콘텐츠에 해당하는 콘텐츠 섹션이 식별되는 사용자 지정 스크러바 컨트롤을 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에 표시된 예제 구현입니다.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 액세스 `Timeline` 의 오브젝트 `MediaPlayer` 사용 `getTimeline` 메서드를 사용합니다.

   다음 `Timeline` 클래스는 현재 가 로드하는 미디어 항목과 연결된 타임라인의 내용과 관련된 정보를 캡슐화합니다 `MediaPlayer` 인스턴스. 다음 `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 대한 액세스를 제공합니다. 다음 `Timeline` 클래스는 목록을 통해 반복기를 제공하는 getter 메서드를 제공합니다. `TimelineMarker` 개체.

1. 목록 반복 `TimelineMarkers` 반환된 정보를 사용하여 타임라인을 구현할 수 있습니다.

       &#39;TimelineMarker&#39; 객체에는 두 가지 정보가 있습니다.
   
   * 타임라인에서 마커의 위치(밀리초)입니다.
   * 타임라인에서 마커의 기간(밀리초)

1. 리스너 콜백 인터페이스 구현 `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 다음을 통해 등록: `Timeline` 개체.

   다음 `Timeline` 객체는 를 호출하여 재생 타임라인에서 발생할 수 있는 변경 사항에 대해 애플리케이션에 알릴 수 있습니다. `OnTimelineUpdated` listener.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```
