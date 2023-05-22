---
description: VOD(video-on-demand) 콘텐츠의 경우, TVSDK는 타임라인 지속 시간이 늘어나도록 기본 콘텐츠에서 광고를 연결하여 광고 브레이크를 삽입합니다.
title: VOD 광고 해결 및 삽입
exl-id: 6f02c7fc-028d-442f-92d4-9efa671b7f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# VOD 광고 해결 및 삽입{#vod-ad-resolving-and-insertion}

VOD(video-on-demand) 콘텐츠의 경우, TVSDK는 타임라인 지속 시간이 늘어나도록 기본 콘텐츠에서 광고를 연결하여 광고 브레이크를 삽입합니다.

재생하기 전에 TVSDK는 알려진 광고를 확인하고, TVSDK에서 반환되는 타임라인에 설명된 대로 기본 콘텐츠에 광고 브레이크를 삽입하고, 필요한 경우 가상 타임라인을 다시 계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **프리롤**: 콘텐츠 앞에 있습니다.
* **미드롤**: 콘텐츠에 있습니다.
* **포스트롤**: 콘텐츠 뒤에 있습니다.

>[!IMPORTANT]
>
>사용자 지정 구현 시 `AdPolicySelector`의 각 유형에 다른 정책을 지정할 수 있습니다. `AdBreakTimelineItem` (프리롤, 미드롤 또는 포스트롤) `AdPolicyInfo`, 의 유형을 기반으로 함 `AdBreakTimelineItem`. 예를 들어 미드롤 컨텐츠가 재생된 후에는 그대로 두고 프리롤 컨텐츠가 재생된 후에는 제거할 수 있습니다.

재생이 시작된 후에는 콘텐츠에서 추가 변경 사항이 발생할 수 없습니다. 광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어 광고 없는 경험을 제공하기 위해 콘텐츠에서 기본 제공 광고를 삭제할 수는 없습니다.
* 대체됨

   예를 들어 기본 제공 광고를 타깃팅된 광고로 대체할 수 없습니다.
