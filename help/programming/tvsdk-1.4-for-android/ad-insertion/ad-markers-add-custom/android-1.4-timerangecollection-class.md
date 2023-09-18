---
description: TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 정렬된 컬렉션 개념을 추상화하고 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.
title: TimeRangeCollection 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# TimeRangeCollection 클래스{#timerangecollection-class}

TimeRangeCollection 유틸리티 클래스는 TimeRange 사양의 정렬된 컬렉션 개념을 추상화하고 메타데이터 인스턴스로 변환하는 서비스를 제공합니다.

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

다음 `type` 매개 변수는 생성자 메서드 시그니처의 첫 번째 위치 매개 변수이며 `TimeRangeCollection#Type` 열거형입니다. 다음은 의 일부입니다. `TimeRangeCollection` 클래스. 이 열거형에 의해 현재 정의된 값은 다음과 같습니다 `MARK_RANGES`, `DELETE_RANGES`, 및 `REPLACE_RANGES`. 다음을 만들 수 있습니다. `TimeRangeCollection` 이 세 가지 유형을 사용하는 개체입니다.
