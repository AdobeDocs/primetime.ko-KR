---
description: 다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 대체할 수 있습니다. 시그널링 모드와 메타데이터의 상이한 조합은 상이한 비헤이비어를 초래한다.
title: 광고 시그널링 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 광고 시그널링 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 대체할 수 있습니다. 시그널링 모드와 메타데이터의 상이한 조합은 상이한 비헤이비어를 초래한다.

>[!TIP]
>
>시간 범위와 광고 시그널링 모드 사이에 충돌이 있을 때, TVSDK는 시간 범위에 우선 순위를 부여한다.

다음 표는 신호 모드 및 메타데이터 조합 동작에 대한 세부 사항을 제공합니다.

**서버 맵**

| **광고 메타데이터** | **해결자 생성됨** | **`PlacementInformations`생성됨** | **결과 비헤이비어** |
|--- |--- |--- |--- |
|  | 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 범위 삭제됨 |
| 삭제, 감사 | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 범위 삭제, 광고 삽입 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 광고 삽입됨 |
| Replace, Auditude | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위 대체됨 |
| 표시 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 범위가 표시되어 있고 광고가 삽입되지 않았습니다. |

**매니페스트 큐**

| 광고 메타데이터 | 해결자 생성됨 | `PlacementInformations` 생성됨 | 결과 비헤이비어 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 광고 삽입됨 |
| 삭제, 감사 | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 범위 삭제, 광고 삽입 |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 범위가 표시되어 있고 광고가 삽입되지 않았습니다. |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 범위 삭제됨 |
| 표시 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Replace, Auditude | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위 대체됨 |

**사용자 정의 시간 범위**

| 광고 메타데이터 | 해결자 생성됨 | `PlacementInformations` 생성됨 | 결과 비헤이비어 |
|--- |--- |--- |--- |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 범위 삭제됨 |
| 삭제, 감사 | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 범위가 삭제되고 광고가 삽입되지 않음 |
| Auditude | Auditude | 없음 | 삽입된 광고 없음 |
| Replace, Auditude | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위가 광고로 대체됨 |
| 표시 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | 사용자 지정 광고, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 범위가 표시되어 있고 광고가 삽입되지 않았습니다. |

**설정되지 않음(기본값)**

| 광고 메타데이터 | 해결자 생성됨 | `PlacementInformations` 생성됨 | 결과 비헤이비어 |
|--- |--- |--- |--- |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 범위 삭제됨 |
| 삭제, 감사 | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 범위 삭제, 광고 삽입 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 광고 삽입됨 |
| Replace, Auditude | 삭제, 감사 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위가 광고로 대체됨 |
| 표시 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
