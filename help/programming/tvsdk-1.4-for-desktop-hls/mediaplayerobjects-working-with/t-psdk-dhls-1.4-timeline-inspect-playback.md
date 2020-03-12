---
description: 현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.
seo-description: 현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.
seo-title: 재생 타임라인 검사
title: 재생 타임라인 검사
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 재생 타임라인 검사{#inspect-the-playback-timeline}

현재 TVSDK에서 재생 중인 선택한 항목과 연결된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 응용 프로그램에서 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크럽 막대 컨트롤을 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에 표시된 구현의 예입니다.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 이 `Timeline` 메서드를 사용하여 에서 개체에 `MediaPlayer` `get` 액세스합니다.

   이 `Timeline` 클래스는 인스턴스가 현재 로드한 미디어 항목과 연결된 타임라인의 컨텐츠와 관련된 정보를 캡슐화합니다 `MediaPlayer` . 이 `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 대한 액세스를 제공합니다. 이 `Timeline` 클래스는 배치된 모든 `TimelineMarker` 객체를 가져오기 위한 getter 메서드를 제공합니다.

1. 목록을 `TimelineMarkers` 반복하고 반환된 정보를 사용하여 타임라인을 구현합니다.

       &#39;TimelineMarker&#39; 개체에는 다음 두 가지 정보가 포함되어 있습니다.
   
   * 타임라인에서 마커의 위치(밀리초 단위)
   * 타임라인에 있는 마커의 지속 시간(밀리초)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```

