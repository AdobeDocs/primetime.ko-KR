---
description: TVSDK에서 재생 중인 현재 선택한 항목과 연결된 타임라인에 대한 설명을 가져올 수 있습니다. 이 기능은 응용 프로그램에서 광고 콘텐츠에 해당하는 콘텐츠 섹션이 식별되는 사용자 지정 스크러바 컨트롤을 표시할 때 가장 유용합니다.
title: 재생 타임라인 Inspect
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 재생 타임라인 Inspect{#inspect-the-playback-timeline}

TVSDK에서 재생 중인 현재 선택한 항목과 연결된 타임라인에 대한 설명을 가져올 수 있습니다. 이 기능은 응용 프로그램에서 광고 콘텐츠에 해당하는 콘텐츠 섹션이 식별되는 사용자 지정 스크러바 컨트롤을 표시할 때 가장 유용합니다.

다음은 다음 스크린샷에 표시된 예제 구현입니다.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 액세스 `Timeline` 의 오브젝트 `MediaPlayer` 사용 `get` 메서드를 사용합니다.

   다음 `Timeline` 클래스는 현재 가 로드하는 미디어 항목과 연결된 타임라인의 내용과 관련된 정보를 캡슐화합니다 `MediaPlayer` 인스턴스. 다음 `Timeline` 클래스는 기본 타임라인의 읽기 전용 보기에 대한 액세스를 제공합니다. 다음 `Timeline` 클래스는 모든 배치를 가져오기 위한 getter 메서드를 제공합니다. `TimelineMarker` 개체.

1. 목록 반복 `TimelineMarkers` 반환된 정보를 사용하여 타임라인을 구현할 수 있습니다.

       &#39;TimelineMarker&#39; 객체에는 두 가지 정보가 있습니다.
   
   * 타임라인에서 마커의 위치(밀리초)입니다.
   * 타임라인에서 마커의 기간(밀리초)

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
