---
description: ReplaceTimeRange 유틸리티 클래스는 CustomRangeMetadata에 사용할 TimeRange 클래스의 확장입니다.
seo-description: ReplaceTimeRange 유틸리티 클래스는 CustomRangeMetadata에 사용할 TimeRange 클래스의 확장입니다.
seo-title: ReplaceTimeRange 클래스
title: ReplaceTimeRange 클래스
uuid: 19c49b26-5096-4429-b30b-bdd2502e3036
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

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

