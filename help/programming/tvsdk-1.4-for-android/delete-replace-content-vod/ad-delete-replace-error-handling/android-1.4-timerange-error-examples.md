---
description: TVSDK는 시간 범위를 적절히 병합하거나 대체하여 잘못된 시간 범위 사양에 응답합니다.
title: 시간 범위 오류 예
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 시간 범위 오류 예{#time-range-error-examples}

TVSDK는 시간 범위를 적절히 병합하거나 대체하여 잘못된 시간 범위 사양에 응답합니다.

다음 예제에서는 교차하는 DELETE 시간 범위 4개가 정의됩니다. TVSDK는 4개의 시간 범위를 1로 병합하므로 실제 삭제 범위는 0-50에서 벗어나 있습니다.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

다음 예에서 4개의 REPLACE 시간 범위가 충돌하는 시간 범위로 정의됩니다. 이 경우 TVSDK는 0-50s를 25개의 광고로 대체합니다. 이후 범위에 충돌이 있기 때문에 정렬 순서에서 첫 번째 대체 지속 시간과 함께 사용됩니다.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```

