---
description: TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-description: TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-title: VOD 광고 확인 및 삽입
title: VOD 광고 확인 및 삽입
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VOD 광고 확인 및 삽입{#vod-ad-resolving-and-insertion}

TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.

재생 전에 TVSDK는 알려진 광고를 확인하고 TVSDK에서 반환되는 타임라인에서 설명한 대로 기본 컨텐츠에 광고 브레이크를 삽입하고 필요한 경우 가상 타임라인을 다시 계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **컨텐츠 앞에 있는 프리롤**.
* **컨텐츠에 있는 중롤**.
* **컨텐츠 뒤에 있는 포스트롤**.

>[!IMPORTANT]
>
>사용자 정의 구현 `AdPolicySelector`시 `AdBreakTimelineItem` 유형을 `AdPolicyInfo``AdBreakTimelineItem`기준으로 각 유형(프리롤, 미드롤 또는 포스트롤)에 다른 정책을 지정할 수 있습니다. 예를 들어, 중간 롤이 재생된 후에 중간 롤의 컨텐츠를 유지할 수 있지만 재생된 후에는 프리롤 컨텐츠를 제거할 수 있습니다.

재생이 시작되면 컨텐츠에서 추가로 변경할 수 없습니다. 광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 경험을 제공하기 위해 컨텐츠에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

