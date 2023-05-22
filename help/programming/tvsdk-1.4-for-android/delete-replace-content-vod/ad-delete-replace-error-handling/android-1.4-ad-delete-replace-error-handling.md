---
description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 재정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.
title: 광고 삭제 및 교체 오류 처리
exl-id: 3147d446-68a1-4e4b-9a29-f464b936d650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 광고 삭제 및 교체 오류 처리{#ad-deletion-and-replacement-error-handling}

TVSDK는 잘못 정의된 시간 범위를 병합하거나 재정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.

TVSDK 거래 `timeRanges` 기본 병합 및 재정렬을 수행하여 오류가 발생했습니다. 먼저 고객이 정의한 시간 범위를 *시작* 시간. 그런 다음 이 정렬 순서를 기반으로 인접한 범위를 병합하고 범위 사이에 하위 집합과 교차가 있으면 결합합니다.

TVSDK는 다음과 같이 시간 범위 오류를 처리합니다.

* 잘못된 순서 - TVSDK가 시간 범위를 재정렬합니다.
* 하위 집합 - TVSDK가 시간 범위 하위 집합을 병합합니다.
* 교차 - TVSDK가 교차하는 시간 범위를 병합합니다.
* 범위 바꾸기 충돌 - TVSDK가 표시되는 가장 이른 시간부터 바꾸기 기간을 선택합니다. `timeRange` 충돌 그룹에 있습니다.

TVSDK는 다음과 같이 광고 메타데이터와의 신호 모드 충돌을 처리합니다.

* 광고 시그널링 모드가 시간 범위 메타데이터와 충돌하는 경우, 시간 범위 메타데이터는 항상 우선순위를 갖는다. 예를 들어 광고 시그널링 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있고 광고 메타데이터에 MARK 시간 범위도 있는 경우 그 결과 범위는 표시되고 광고가 삽입되지 않는다는 동작이 됩니다.
* REPLACE 범위의 경우 시그널링 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있으면 REPLACE 범위에 지정된 대로 범위가 대체되며 서버 맵 또는 매니페스트 큐를 통한 광고 삽입은 없습니다. 다음을 참조하십시오 [광고 신호 모드](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

서버가 유효한 을 반환하지 않는 경우 `AdBreaks`:

* TVSDK는 다음을 생성하고 처리합니다. `NOPTimelineOperation` 을 위해 `AdBreak`. 광고가 재생되지 않습니다.

라이브 스트림이 있는 시간 범위의 경우:

* 이 C3 광고 삭제/대체 기능은 VOD에 대해서만 지원되지만 광고 메타데이터에 지정된 경우 라이브 스트림에 대해서도 시간 범위가 처리됩니다.

## 시간 범위 오류 예 {#time-range-error-examples}

TVSDK가 시간 범위를 적절하게 병합하거나 교체하여 잘못된 시간 범위 지정에 응답합니다.

다음 예에서는 네 개의 교차 DELETE 시간 범위가 정의됩니다. TVSDK는 네 개의 시간 범위를 하나로 병합하므로 실제 삭제 범위는 0~50초입니다.

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

다음 예에서는 충돌하는 시간 범위로 4개의 REPLACE 시간 범위가 정의됩니다. 이 경우 TVSDK는 0-50초를 25초 광고로 대체합니다. 이후 범위에 충돌이 있으므로 정렬 순서의 첫 번째 대체 기간과 일치합니다.

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
