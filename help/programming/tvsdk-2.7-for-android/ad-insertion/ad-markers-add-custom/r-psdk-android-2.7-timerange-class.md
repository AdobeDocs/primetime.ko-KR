---
description: 사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 TimeRange 지정 세트를 TVSDK에 전달할 수 있습니다.
title: TimeRange 클래스
exl-id: 623b287e-4441-4290-a332-713a5e8282b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# TimeRange 클래스 {#timerange-class}

사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 TimeRange 지정 세트를 TVSDK에 전달할 수 있습니다.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

각 `TimeRange` 세트의 사양은 TVSDK에 의해 내부적으로 유지되며 광고 관련 기간으로 적절하게 표시되어야 하는 재생 타임라인의 세그먼트를 나타냅니다.

다음 `TimeRange` 클래스는 타임라인의 시작 위치와 끝 위치를 노출하는 간단한 데이터 구조입니다. 이 두 개의 읽기 전용 속성은 재생 타임라인의 시간 범위 개념을 요약합니다.

>[!TIP]
>
>두 값은 밀리초 단위로 표시됩니다.

다음은 의 요약입니다 `TimeRange` 클래스:

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```
