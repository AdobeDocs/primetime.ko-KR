---
description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 순서를 변경하여 특정 문제에 따라 시간 범위 오류를 처리합니다.
seo-description: TVSDK는 잘못 정의된 시간 범위를 병합하거나 순서를 변경하여 특정 문제에 따라 시간 범위 오류를 처리합니다.
seo-title: 광고 삭제 및 교체 오류 처리
title: 광고 삭제 및 교체 오류 처리
uuid: 9a951bc4-b372-4655-8510-3f474171415d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 개요 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK는 잘못 정의된 시간 범위를 병합하거나 순서를 변경하여 특정 문제에 따라 시간 범위 오류를 처리합니다.

TVSDK는 기본 병합 및 순서 변경을 통해 `timeRanges` 오류를 관리합니다. 첫 번째, 플레이어는 *시작* 시간에 따라 고객 정의 시간 범위를 정렬합니다. 이 정렬 순서를 기반으로, 범위 사이에 하위 세트와 교차가 있는 경우 TVSDK는 인접한 범위를 병합하고 이러한 범위에 참여합니다.

TVSDK는 다음 옵션을 사용하여 시간 범위 오류를 처리합니다.

* **순서가 잘못된** TVSDK는 시간 범위를 다시 정렬합니다.

* **하위** 세트 TVSDK는 시간 범위 하위 집합을 병합합니다.

* **TVSDK** 교차에서 교차하는 시간 범위를 병합합니다.

* **바꾸기 범위 충돌** TVSDK는 충돌 그룹에 표시되는 가장 빠른 `timeRange` 시간부터 교체 기간을 선택합니다.

TVSDK는 다음과 같은 방법으로 광고 메타데이터와 신호 모드 충돌을 처리합니다.

* 광고 신호 모드가 시간 범위 메타데이터와 충돌하는 경우 시간 범위 메타데이터에는 항상 우선 순위가 있습니다.

   예를 들어 광고 신호 모드가 서버 맵 또는 매니페스트 큐로 설정되고 광고 메타데이터에 MARK 시간 범위도 있는 경우 결과 동작은 범위가 표시되고 광고가 삽입되지 않는다는 것입니다.
* REPLACE 범위의 경우 신호 모드가 서버 맵 또는 매니페스트 큐로 설정된 경우, 범위는 REPLACE 범위에 지정된 대로 대체되며, 서버 맵 또는 매니페스트 큐를 통한 광고 삽입이 없습니다.

   자세한 내용은 광고 삽입 및 *삭제에 대한* 효과의 신호 모드/메타데이터 조합 동작 [표를 참조하십시오....](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

다음 사항을 기억하십시오.

* 서버가 유효한 결과를 반환하지 않으면 TVSDK가 빈 AdBreak에 대한 `AdBreaks``NOPTimelineOperation` a를 생성하고 처리하며 광고가 재생되지 않습니다.

* C3 광고 삭제/대체는 VOD에만 지원되지만 광고 메타데이터에 지정된 경우 실시간 스트림에도 시간 범위가 처리됩니다.

