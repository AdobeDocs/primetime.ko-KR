---
description: TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.
seo-description: TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.
seo-title: VOD 광고 해결 및 삽입
title: VOD 광고 해결 및 삽입
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# VOD 광고 확인 및 삽입{#vod-ad-resolving-and-insertion}

TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.

재생 전에 TVSDK는 TVSDK에서 반환되는 타임라인에서 설명한 대로 기본 컨텐츠에 알려진 광고를 확인하고 삽입하며 필요에 따라 가상 타임라인을 재계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **프리롤** - 컨텐츠 앞에 있습니다.
* **컨텐츠에 있는 중롤**.
* **컨텐츠 뒤에 있는 포스트롤**.

>[!IMPORTANT]
>
>사용자 지정 `AdPolicySelector`을(를) 구현할 때 `AdBreakTimelineItem`의 유형에 따라 `AdPolicyInfo`의 각 유형(프리롤, 미드롤 또는 포스트롤)에 다른 정책을 지정할 수 있습니다. `AdBreakTimelineItem` 예를 들어, 중간 롤이 재생된 후에는 중간 롤의 컨텐츠를 유지할 수 있지만 재생된 후에는 프리롤 컨텐츠를 제거할 수 있습니다.

재생이 시작되면 컨텐츠에 추가 변경 사항이 발생하지 않습니다. 광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 환경을 제공하기 위해 컨텐트에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

