---
description: 사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 일련의 TimeRange 사양을 TVSDK로 전달할 수 있습니다.
seo-description: 사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 일련의 TimeRange 사양을 TVSDK로 전달할 수 있습니다.
seo-title: TimeRange 클래스
title: TimeRange 클래스
uuid: adf4f1ad-6b3b-48ac-a388-ee1fd54f770b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# TimeRange 클래스{#timerange-class}

사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 일련의 TimeRange 사양을 TVSDK로 전달할 수 있습니다.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

세트의 각 TimeRange 사양은 TVSDK에서 내부적으로 유지 관리되고 광고 관련 기간으로 적절하게 표시되어야 하는 재생 타임라인의 세그먼트를 나타냅니다.

이 `TimeRange` 클래스는 타임라인에서 시작 위치와 끝 위치를 표시하는 간단한 데이터 구조입니다. 이러한 두 개의 읽기 전용 속성은 재생 타임라인에서 시간 범위에 대한 개념을 추상화합니다.

>[!TIP]
>
>두 값 모두 밀리초 단위로 표현됩니다.

다음은 이 `TimeRange` 클래스의 요약입니다.

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

