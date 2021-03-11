---
description: 사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 TimeRange 사양 집합을 TVSDK로 전달할 수 있습니다.
title: TimeRange 클래스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# TimeRange 클래스{#timerange-class}

사용자 지정 광고 마커를 사용하면 타임라인 세그먼트를 나타내는 TimeRange 사양 집합을 TVSDK로 전달할 수 있습니다.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

세트에 있는 각 `TimeRange` 사양은 TVSDK에서 내부적으로 유지 관리되는 재생 타임라인의 세그먼트를 나타내며 광고 관련 기간으로 적절하게 표시되어야 합니다.

`TimeRange` 클래스는 타임라인에서 시작 위치와 끝 위치를 표시하는 간단한 데이터 구조입니다. 이러한 두 읽기 전용 속성은 재생 타임라인에서 시간 범위에 대한 개념을 추상화합니다.

>[!TIP]
>
>두 값 모두 밀리초 단위로 표시됩니다.

다음은 TimeRange 클래스의 요약입니다.

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```

