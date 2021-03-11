---
description: TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 순서가 지정된 컬렉션의 개념을 추상화하고 자신을 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.
title: TimeRangeCollection 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# TimeRangeCollection 클래스{#timerangecollection-class}

TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 순서가 지정된 컬렉션의 개념을 추상화하고 자신을 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

생성자 메서드 서명의 첫 번째 위치 매개 변수인 `type` 매개 변수는 `TimeRangeCollection#Type` 열거형의 인스턴스입니다. 이것은 `TimeRangeCollection` 클래스의 일부입니다. 이 열거에 의해 현재 정의된 값은 `MARK_RANGES`, `DELETE_RANGES` 및 `REPLACE_RANGES`입니다. 이러한 3가지 유형을 사용하여 `TimeRangeCollection` 개체를 만들 수 있습니다.
