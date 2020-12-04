---
description: ReplaceTimeRange 유틸리티 클래스는 CustomRangeMetadata에 사용할 TimeRange 클래스의 확장입니다.
seo-description: ReplaceTimeRange 유틸리티 클래스는 CustomRangeMetadata에 사용할 TimeRange 클래스의 확장입니다.
seo-title: ReplaceTimeRange 클래스
title: ReplaceTimeRange 클래스
uuid: d554c17a-2bdc-4c4a-bb8f-2d357511bb32
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# ReplaceTimeRange 클래스 {#replacetimerange-class}

ReplaceTimeRange 유틸리티 클래스는 CustomRangeMetadata에 사용할 TimeRange 클래스의 확장입니다.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
