---
description: 이 예는 재생 타임라인에 TimeRange 사양을 포함하는 권장 방법을 보여 줍니다.
title: 타임라인에 TimeRange 광고 마커 배치
exl-id: a4d45395-38a4-4345-9ba3-87cd9200b9f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 타임라인에 TimeRange 광고 마커 배치 {#place-timerange-ad-markers-on-the-timeline}

이 예는 재생 타임라인에 TimeRange 사양을 포함하는 권장 방법을 보여 줍니다.

1. 대역 외 광고 위치 정보를 다음 목록으로 변환 `TimeRange` 사양(즉, 의 인스턴스) `TimeRange` class).
1. 다음 집합 사용 `TimeRange` 인스턴스 채우기 위한 세부 항목 `TimeRangeCollection` 클래스.
1. 메타데이터 인스턴스를 전달합니다. 이 인스턴스는 `TimeRangeCollection` 인스턴스: `replaceCurrentItem` 메서드(의 일부 `MediaPlayer` 인터페이스).
1. TVSDK가 다음을 대기하여 PREPARED 상태로 전환될 때까지 대기 `PlaybackEventListener#onPrepared` 트리거할 콜백입니다.
1. 를 호출하여 비디오 재생 시작 `play()` 메서드(의 일부 `MediaPlayer` 인터페이스).

* 타임라인 충돌 처리: 다음과 같은 경우가 있을 수 있습니다. `TimeRange` 세부 항목이 재생 타임라인에서 겹칩니다. 예를 들어 시작 위치의 값은 `TimeRange` 사양은 이미 배치된 끝 위치의 값보다 낮을 수 있습니다. 이 경우 TVSDK는 위반의 시작 위치를 자동으로 조정합니다 `TimeRange` 타임라인 충돌을 방지하기 위한 사양. 이 조정을 통해 `TimeRange` 가 원래 지정된 것보다 짧아집니다. 조정이 너무 극단적이어서 `TimeRange` 기간이 0ms인 경우 TVSDK는 문제가 되는 항목을 자동으로 삭제합니다 `TimeRange` 사양.

* 날짜 `TimeRange` 사용자 지정 광고 브레이크에 대한 사양이 제공되면 TVSDK는 이 사양을 광고 브레이크 내에 그룹화된 광고로 번역합니다. TVSDK는 인접 항목을 찾습니다. `TimeRange` 세부 항목을 지정하고 이를 별도의 ad break로 클러스터링합니다. 다른 시간 범위와 이웃하지 않는 시간 범위가 있는 경우 단일 광고가 포함된 광고 브레이크로 변환됩니다.

* 로드 중인 미디어 플레이어 항목이 VOD 자산을 가리킨다고 가정합니다. TVSDK는 애플리케이션이 메타데이터에 포함된 미디어 리소스를 로드하려고 할 때마다 이를 확인합니다 `TimeRange` 사용자 지정 광고 마커 기능의 컨텍스트에서만 사용할 수 있는 사양입니다. 기본 자산이 VOD 유형이 아닌 경우 TVSDK 라이브러리에서 예외가 발생합니다.

* 사용자 지정 광고 마커를 처리할 때 TVSDK는 다른 광고 해결 메커니즘을 비활성화합니다(Adobe Primetime 광고 의사 결정(이전 이름: Auditude) 또는 기타 광고 프로비저닝 시스템을 통해). TVSDK에서 제공하는 다양한 ad-resolver 모듈 또는 사용자 지정 ad-markers 메커니즘을 사용할 수 있습니다. 사용자 지정 광고 마커 API를 사용하는 경우 광고 콘텐츠는 이미 해결된 것으로 간주되며 타임라인에 배치됩니다.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

다음 코드 스니펫은 세 가지 코드 조각이 모여 있는 간단한 예제를 제공합니다 `TimeRange` 사양은 타임라인에 사용자 지정 광고 마커로 배치됩니다.

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
