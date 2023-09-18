---
description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 재정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.
title: 광고 삭제 및 교체 오류 처리
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 개요 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK는 잘못 정의된 시간 범위를 병합하거나 재정렬하여 특정 문제에 따라 시간 범위 오류를 처리합니다.

TVSDK 관리 `timeRanges` 기본 병합 및 재정렬 프로세스를 통해 오류가 발생했습니다. 먼저 플레이어는 고객 정의 시간 범위를 *시작* 시간. 이 정렬 순서에 따라 범위 사이에 하위 집합과 교차가 있으면 TVSDK는 인접한 범위를 병합하고 이 범위를 연결합니다.

TVSDK는 다음 옵션을 사용하여 시간 범위 오류를 처리합니다.

* **잘못된 항목** TVSDK는 시간 범위를 재정렬합니다.

* **하위 집합** TVSDK가 시간 범위 하위 집합을 병합합니다.

* **교차** TVSDK는 교차하는 시간 범위를 병합합니다.

* **범위 바꾸기 충돌** TVSDK가 가장 이른 시간부터 바꾸기 기간을 선택합니다. `timeRange` 충돌 그룹에 나타납니다.

TVSDK는 다음과 같은 방법으로 광고 메타데이터와의 신호 모드 충돌을 처리합니다.

* 광고 시그널링 모드가 시간 범위 메타데이터와 충돌하는 경우, 시간 범위 메타데이터는 항상 우선순위를 갖는다.

  예를 들어 광고 시그널링 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있고 광고 메타데이터에 MARK 시간 범위도 있는 경우 그 결과 범위는 표시되고 광고가 삽입되지 않는다는 동작이 됩니다.
* REPLACE 범위의 경우 신호 처리 모드가 서버 맵 또는 매니페스트 큐로 설정되어 있으면 REPLACE 범위에 지정된 대로 범위가 대체되며 서버 맵 또는 매니페스트 큐를 통한 광고 삽입은 없습니다.

  자세한 내용은 *신호 모드/메타데이터 조합 동작* 테이블 위치 [광고 삽입 및 광고 신호 모드에서 삭제에 미치는 영향...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

다음 사항을 기억하십시오.

* 서버가 유효한 을 반환하지 않는 경우 `AdBreaks`, TVSDK는 를 생성하고 처리합니다. `NOPTimelineOperation` 빈 AdBreak에 대해 광고를 재생하지 않습니다.

* C3 광고 삭제/대체는 VOD에 대해서만 지원되지만 광고 메타데이터에 지정된 경우 라이브 스트림에 대해서도 시간 범위가 처리됩니다.
