---
description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 순서를 변경하면서 특정 문제에 따라 시간 범위 오류를 처리합니다.
title: 광고 삭제 및 교체 오류 처리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 광고 삭제 및 교체 오류 처리{#ad-deletion-and-replacement-error-handling}

TVSDK는 잘못 정의된 시간 범위를 병합하거나 순서를 변경하면서 특정 문제에 따라 시간 범위 오류를 처리합니다.

TVSDK는 기본 병합 및 순서 변경을 수행하여 `timeRanges` 오류를 처리합니다. 첫째, 고객 정의 시간 범위를 *begin* 시간으로 정렬합니다. 이 정렬 순서를 기반으로 인접한 범위를 병합하고 범위 사이에 하위 세트와 교차가 있으면 결합합니다.

TVSDK는 다음과 같이 시간 범위 오류를 처리합니다.

* 순서가 잘못됨 - TVSDK가 시간 범위를 재주문합니다.
* 하위 세트 - TVSDK가 시간 범위 하위 집합을 병합합니다.
* 교차 - TVSDK가 교차하는 시간 범위를 병합합니다.
* 바꾸기 범위 충돌 - TVSDK는 충돌 그룹의 가장 빨리 나타나는 `timeRange`에서 교체 기간을 선택합니다.

TVSDK는 다음과 같이 광고 메타데이터와 신호 모드 충돌을 처리합니다.

* 광고 신호 모드가 시간 범위 메타데이터와 충돌하는 경우 시간 범위 메타데이터는 항상 우선 순위를 갖습니다. 예를 들어 광고 신호 모드가 서버 맵 또는 매니페스트 큐로 설정되고 광고 메타데이터에 MARK 시간 범위도 있는 경우 결과 동작은 범위가 표시되고 광고가 삽입되지 않는다는 것입니다.
* REPLACE 범위의 경우 신호 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있으면 REPLACE 범위에 지정된 대로 범위가 대체되고 서버 맵 또는 매니페스트 큐를 통한 광고 삽입이 없습니다. [광고 신호 모드](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md)를 참조하십시오.

서버에서 올바른 `AdBreaks`을(를) 반환하지 않는 경우:

* TVSDK는 빈 `AdBreak`에 대해 `NOPTimelineOperation`을(를) 생성하고 처리합니다. 광고 재생 없음

실시간 스트림이 있는 시간 범위의 경우:

* 이 C3 광고 삭제/바꾸기 기능은 VOD에만 지원되도록 만들어졌지만 광고 메타데이터에 지정된 경우 실시간 스트림에도 대해 시간 범위가 처리됩니다.

## 시간 범위 오류 예 {#time-range-error-examples}

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
