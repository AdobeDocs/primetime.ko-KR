---
description: TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 정렬된 컬렉션 개념을 추상화하고 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.
title: TimeRangeCollection 클래스
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# TimeRangeCollection 클래스{#timerangecollection-class}

TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 정렬된 컬렉션 개념을 추상화하고 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

컬렉션 유형에 대해 정의된 값은 다음과 같습니다 `MARK_RANGES`, `DELETE_RANGES`, 및 `REPLACE_RANGES`. 다음을 만들 수 있습니다. `TimeRangeCollection`는 이 세 가지 유형을 사용합니다.
