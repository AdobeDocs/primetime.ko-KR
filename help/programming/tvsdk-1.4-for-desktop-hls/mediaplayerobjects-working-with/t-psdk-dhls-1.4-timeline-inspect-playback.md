---
description: TVSDK에서 재생되는 현재 선택한 항목과 연관된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크러빙 막대 컨트롤을 응용 프로그램에 표시할 때 가장 유용합니다.
title: Inspect 재생 타임라인
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect 재생 타임라인{#inspect-the-playback-timeline}

TVSDK에서 재생되는 현재 선택한 항목과 연관된 타임라인에 대한 설명을 볼 수 있습니다. 이 기능은 광고 컨텐츠에 해당하는 컨텐츠 섹션이 식별되는 사용자 정의 스크러빙 막대 컨트롤을 응용 프로그램에 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에 표시된 구현의 예입니다.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. `get` 메서드를 사용하여 `MediaPlayer`의 `Timeline` 개체에 액세스합니다.

   `Timeline` 클래스는 현재 `MediaPlayer` 인스턴스에서 불러온 미디어 항목과 연결된 타임라인의 컨텐츠와 관련된 정보를 캡슐화합니다. `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 대한 액세스를 제공합니다. `Timeline` 클래스는 가져온 모든 `TimelineMarker` 개체를 가져오기 위한 getter 메서드를 제공합니다.

1. `TimelineMarkers` 목록을 반복하고 반환된 정보를 사용하여 타임라인을 구현합니다.

       &#39;TimelineMarker&#39; 객체에는 다음과 같은 두 가지 정보가 포함됩니다.
   
   * 타임라인의 마커 위치(밀리초 단위)
   * 타임라인의 마커 지속 시간(밀리초)

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

