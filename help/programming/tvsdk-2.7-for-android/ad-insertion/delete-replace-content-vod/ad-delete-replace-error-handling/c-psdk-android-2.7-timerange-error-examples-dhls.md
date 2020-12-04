---
description: TVSDK는 시간 범위를 적절하게 병합하거나 대체하여 잘못된 시간 범위 사양에 응답합니다.
seo-description: TVSDK는 시간 범위를 적절하게 병합하거나 대체하여 잘못된 시간 범위 사양에 응답합니다.
seo-title: 시간 범위 오류 예
title: 시간 범위 오류 예
uuid: f6cc1e61-8f42-4559-b643-2134180a8c5e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 시간 범위 오류 예{#time-range-error-examples}

TVSDK는 시간 범위를 적절하게 병합하거나 대체하여 잘못된 시간 범위 사양에 응답합니다.

**DELETE 시간 범위**

다음 예에서는 네 개의 교차하는 DELETE 시간 범위가 정의됩니다. TVSDK는 4개의 시간 범위를 1개로 병합하므로 실제 삭제 범위는 0-50입니다.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**REPLACE time range**

다음 예에서는 네 개의 REPLACE 시간 범위가 충돌하는 시간 범위로 정의됩니다. 이 경우 TVSDK는 0-50s 광고를 25개의 광고로 대체합니다. 이후 범위에 충돌이 있기 때문에 정렬 순서에서 첫 번째 대체 기간과 함께 사용됩니다.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```

