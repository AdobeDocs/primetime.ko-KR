---
description: TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 순서가 지정된 컬렉션의 개념을 추상화하고 자신을 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.
title: TimeRangeCollection 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# TimeRangeCollection 클래스{#timerangecollection-class}

TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 순서가 지정된 컬렉션의 개념을 추상화하고 자신을 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

컬렉션 유형에 대해 정의된 값은 `MARK_RANGES`, `DELETE_RANGES` 및 `REPLACE_RANGES`입니다. 이러한 3가지 유형을 사용하여 `TimeRangeCollection`s를 만들 수 있습니다.
