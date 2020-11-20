---
description: 이 예는 재생 타임라인에 TimeRange 사양을 포함하는 권장 방법을 보여줍니다.
seo-description: 이 예는 재생 타임라인에 TimeRange 사양을 포함하는 권장 방법을 보여줍니다.
seo-title: 타임라인에 시간 범위 광고 마커 배치
title: 타임라인에 시간 범위 광고 마커 배치
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: fd21a29bb186238142d43e0277bbf92f8406f6f7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 타임라인에 시간 범위 광고 마커 배치 {#place-timerange-ad-markers-on-the-timeline}

이 예는 재생 타임라인에 TimeRange 사양을 포함하는 권장 방법을 보여줍니다.

1. 대역 외 광고 배치 정보를 사양 목록(즉, 클래스 인스턴스) `TimeRange` 으로 `TimeRange` 변환합니다.
1. 사양 집합을 `TimeRange` 사용하여 클래스의 인스턴스를 `TimeRangeCollection` 채웁니다.
1. 인스턴스에서 얻을 수 있는 메타데이터 인스턴스 `TimeRangeCollection` 를 메서드(인터페이스의 `replaceCurrentItem` 일부)로 `MediaPlayer` 전달합니다.
1. 콜백이 트리거될 때까지 대기하여 TVSDK가 준비된 상태로 `PlaybackEventListener#onPrepared` 전환할 때까지 기다립니다.
1. 메서드(인터페이스의 일부)를 호출하여 비디오 재생을 `play()` `MediaPlayer` 시작합니다.

* 타임라인 충돌 처리:일부 사양이 재생 타임라인에서 겹치는 경우가 있을 수 있습니다. `TimeRange` 예를 들어 사양에 해당하는 시작 위치의 값은 이미 배치된 끝 위치의 값보다 `TimeRange` 작을 수 있습니다. 이 경우 TVSDK는 시간표 충돌을 방지하기 위해 잘못된 사양의 시작 위치를 자동으로 `TimeRange` 조정합니다. 이 조정을 통해 새 `TimeRange` 기능은 원래 지정된 것보다 짧습니다. 조정이 너무 심해서 지속 시간이 0ms `TimeRange` 로 이어질 경우 TVSDK가 자동으로 잘못된 `TimeRange` 사양을 삭제합니다.

* 사용자 지정 광고 `TimeRange` 중단에 대한 사양이 제공되면 TVSDK는 이러한 광고를 광고 중단 내에 그룹화된 광고로 변환합니다. TVSDK는 서로 다른 `TimeRange` 사양을 찾아 별도의 광고 중단으로 클러스터링합니다. 다른 시간 범위와 인접하지 않은 시간 범위가 있는 경우 단일 광고가 포함된 광고 나누기로 변환됩니다.

* VOD 자산에 포인트를 로드하고 있는 미디어 플레이어 항목이 있다고 가정합니다. TVSDK는 애플리케이션이 사용자 지정 광고 마커 기능의 컨텍스트에서만 사용할 수 있는 메타데이터가 포함된 미디어 리소스를 로드하려고 할 때마다 이를 확인합니다. `TimeRange` 기본 자산이 VOD 유형이 아닌 경우 TVSDK 라이브러리는 예외를 throw합니다.

* 사용자 지정 광고 마커를 처리할 때 TVSDK는 기타 광고 해결 메커니즘(Adobe Primetime 광고 결정(이전의 Auditude) 또는 기타 광고 제공 시스템을 통해)을 비활성화합니다. TVSDK에서 제공하는 다양한 광고 해결 프로그램 모듈 또는 사용자 지정 광고 마커 메커니즘을 사용할 수 있습니다. 사용자 지정 광고 마커 API를 사용하는 경우 광고 컨텐츠는 이미 해결된 것으로 간주되어 타임라인에 배치됩니다.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

다음 코드 조각은 사용자 지정 광고 마커로 타임라인에 세 가지 `TimeRange` 사양 세트가 배치되는 간단한 예를 제공합니다.

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
