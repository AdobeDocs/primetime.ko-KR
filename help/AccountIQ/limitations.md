---
title: 제한 사항 및 알려진 문제
description: 제품의 알려진 문제.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 알려진 문제 및 제한 사항 {#known-issues}

Adobe은 오퍼링을 통해 강력한 기능과 원활한 사용자 경험을 제공하기 위해 노력하고 있습니다. 계정 IQ의 현재 버전(버전 1.1)은 높은 신뢰도로 스트리밍 공급자에 대한 사용 및 구독 공유 분석을 제공합니다. 그러나 다음 제한 사항은 향후 릴리스 버전에서 해결될 예정입니다.

* 대시보드 또는 보고서 페이지에서 집단을 정의할 때 현재 다음과 같은 지표를 추가하는 선택 사항이 없습니다 **장치 수** 세그먼트를 세분화하기 위해 다음을 수행하십시오. 이 기능은 가까운 시일 내에 제공될 예정입니다.

* 개별 계정에 대한 공유 점수를 추정할 때 계정 IQ는 회사에서 높은 신뢰도로 공유하는 작업을 수행할 수 있도록 하는 보수적인 접근 방식을 사용합니다. 그러나 이 접근 방식은 여러 계정에서 집계할 때 공유의 총 양을 과소평가하는 경향이 있습니다.

* 다음 [전체 공유 점수](/help/AccountIQ/dashboard.md#overall-sharing-score) 현재 유일한 요소 [공유 수준](/help/AccountIQ/dashboard.md#sharing-level) 및 [공유 계정의 사용](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). 향후 버전은 추가 지표를 가능하게 됩니다.

* 대시보드 또는 보고서 페이지에서 집단을 정의할 때 현재 MVPD 및 채널에 대한 선택기에 검색 메커니즘이 없습니다.

* 대시보드 또는 보고서 페이지에서 집단을 정의할 때는 최대 10개의 MVPD 및 프로그래머(또는 개별 채널)만 선택할 수 있는 제한이 있습니다.

* 계정 통계를 내보내는 옵션은 현재 1000개의 계정을 내보내는 것으로 제한됩니다.

* 선택할 수 있는 옵션 [세그먼트 유형](#segment-type) 작업 정의 시 **고정 계정 수**. 다음 **변수 계정 수** 옵션은 곧 제공될 예정입니다.

* 왼쪽 탐색 메뉴의 벤치마킹, 감지 모델, 세그먼트, 스냅샷 및 규칙 섹션은 현재 비활성화되어 있으며 향후 버전에서 사용할 수 있습니다.

* 생성 시 [작업](/help/AccountIQ/operation-affecting-user-segment.md), 에서는 두 가지 종류의 [작업](/help/AccountIQ/operation-affecting-user-segment.md) 현재 — 동시 실행 병합 규칙 및 외부 작업

* 현재 작업을 만들고 [예약됨](/help/AccountIQ/operation-affecting-user-segment.md#action). 향후 버전을 사용하면 일시 중지, 다시 시작 및 완전히 관리할 수 있습니다.

* 사용되는 데이터 세트가 제한되므로 격리 모드는 공유량을 정확히 반영하지 않습니다. 따라서 격리 모드의 MVPD는 다른 MVPD와 비교할 수 없습니다. <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* 새 [세그먼트](/help/AccountIQ/segments-timeframe.md) 작업에 대해 지표를 추가할 수 있습니다. 하지만 저장된 세그먼트를 선택하면 세그먼트를 세분화하기 위해 지표를 더 추가할 수 없습니다.

* 세부기간 및 시간대 선택기는 1주 또는 1개월로 제한됩니다. 즉, 데이터를 1주 또는 1개월에서만 평가할 수 있습니다.

* 사전 정의된 간격은 현재 세부기간 및 시간대 선택기에서 비활성화되며 향후 버전에서 사용할 수 있습니다.
