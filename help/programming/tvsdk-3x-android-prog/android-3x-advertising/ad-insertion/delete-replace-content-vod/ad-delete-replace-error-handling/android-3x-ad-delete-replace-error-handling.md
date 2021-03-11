---
description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 다시 정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.
title: 광고 삭제 및 교체 오류 처리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 광고 삭제 및 교체 오류 처리 {#ad-deletion-and-replacement-error-handling}

TVSDK는 잘못 정의된 시간 범위를 병합하거나 다시 정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.

TVSDK는 기본 병합 및 순서 변경 프로세스를 통해 `timeRanges` 오류를 관리합니다. 먼저, 플레이어는 고객이 정의한 시간 범위를 *begin* 시간으로 정렬합니다. 이 정렬 순서를 기반으로, 범위 사이에 하위 세트와 교차가 있는 경우 TVSDK는 인접한 범위를 병합하고 이러한 범위를 연결합니다.

TVSDK는 다음 옵션을 사용하여 시간 범위 오류를 처리합니다.

* **주문** 외 TVSDK는 시간 범위를 재주문합니다.

* **** SubsetTVSDK는 시간 범위 하위 집합을 병합합니다.

* **IntersectTVSDK** 는 교차하는 시간 범위를 병합합니다.

* **범위** 바꾸기 충돌TVSDK는 충돌 그룹에 나타나는 가장 빠른 시간 `timeRange` 에서 바꾸기 기간을 선택합니다.

TVSDK는 다음과 같은 방식으로 광고 메타데이터와 신호 모드 충돌을 처리합니다.

* 광고 신호 모드가 시간 범위 메타데이터와 충돌하는 경우 시간 범위 메타데이터는 항상 우선 순위를 갖습니다.

   예를 들어 광고 신호 모드가 서버 맵 또는 매니페스트 큐로 설정되고 광고 메타데이터에 MARK 시간 범위도 있는 경우 결과 동작은 범위가 표시되고 광고가 삽입되지 않는다는 것입니다.
* REPLACE 범위의 경우 신호 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있으면 REPLACE 범위에 지정된 대로 범위가 대체되고 서버 맵 또는 매니페스트 큐를 통한 광고 삽입이 없습니다.

   자세한 내용은 [광고 신호 모드에서 광고 삽입 및 삭제 효과](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md)의 *신호 모드/메타데이터 조합 비헤이비어* 표를 참조하십시오.

다음 사항을 기억하십시오.

* 서버가 유효한 `AdBreaks`을(를) 반환하지 않으면 TVSDK가 빈 AdBreak에 대해 `NOPTimelineOperation`을(를) 생성하고 처리하며 광고가 재생되지 않습니다.

* C3 광고 삭제/바꾸기는 VOD에만 지원되도록 의도한 것이지만 광고 메타데이터에 지정된 경우 실시간 스트림에 대해서도 시간 범위가 처리됩니다.
