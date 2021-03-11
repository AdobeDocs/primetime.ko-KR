---
description: 다른 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터의 서로 다른 조합으로 인해 다른 동작이 발생합니다.
title: 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

다른 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터의 서로 다른 조합으로 인해 다른 동작이 발생합니다.

>[!TIP]
>
>시간 범위와 광고 신호 모드 간에 충돌이 발생하는 경우 TVSDK는 시간 범위 우선 순위를 제공합니다.

다음 표는 신호 모드 및 메타데이터 조합 비헤이비어에 대한 세부 정보를 제공합니다.

**서버 맵**

| **광고 메타데이터** | **만든 해상도** | **`PlacementInformations`created** | **결과 동작** |
|--- |--- |--- |--- |
|  | 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 삭제된 범위 |
| 삭제, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 삭제된 범위, 삽입된 광고 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 삽입된 광고 |
| 바꾸기, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위가 대체됨 |
| 마크 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위, 삽입된 광고 없음 |

**매니페스트 큐**

| 광고 메타데이터 | 만든 해상도 | `PlacementInformations` created | 결과 동작 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 삽입된 광고 |
| 삭제, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 삭제된 범위, 삽입된 광고 |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위, 삽입된 광고 없음 |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 삭제된 범위 |
| 마크 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| 바꾸기, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 범위가 대체됨 |

**사용자 지정 시간 범위**

| 광고 메타데이터 | 만든 해상도 | `PlacementInformations` created | 결과 동작 |
|--- |--- |--- |--- |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 삭제된 범위 |
| 삭제, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 삭제된 범위, 광고가 삽입되지 않음 |
| Auditude | Auditude | 없음 | 삽입된 광고 없음 |
| 바꾸기, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 광고로 대체된 범위 |
| 마크 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | 사용자 지정 광고, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위, 삽입된 광고 없음 |

**설정되지 않음(기본값)**

| 광고 메타데이터 | 만든 해상도 | `PlacementInformations` created | 결과 동작 |
|--- |--- |--- |--- |
| 삭제 | 삭제 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 삭제된 범위 |
| 삭제, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 삭제된 범위, 삽입된 광고 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 삽입된 광고 |
| 바꾸기, Auditude | 삭제, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 광고로 대체된 범위 |
| 마크 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 표시된 범위 |