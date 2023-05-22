---
description: TVSDK가 시간 범위를 적절하게 병합하거나 교체하여 잘못된 시간 범위 지정에 응답합니다.
title: 시간 범위 오류 예
exl-id: bf634623-8770-4090-96d7-8facdf4cfc42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 시간 범위 오류 예 {#time-range-error-examples}

TVSDK가 시간 범위를 적절하게 병합하거나 교체하여 잘못된 시간 범위 지정에 응답합니다.

**DELETE 시간 범위**

다음 예에서는 네 개의 교차 DELETE 시간 범위가 정의됩니다. TVSDK는 네 개의 시간 범위를 하나로 병합하므로 실제 삭제 범위는 0~50초입니다.

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

**바꾸기 시간 범위**

다음 예에서는 충돌하는 시간 범위로 4개의 REPLACE 시간 범위가 정의됩니다. 이 경우 TVSDK는 0-50초를 25초 광고로 대체합니다. 이후 범위에 충돌이 있으므로 정렬 순서의 첫 번째 대체 기간과 일치합니다.

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
