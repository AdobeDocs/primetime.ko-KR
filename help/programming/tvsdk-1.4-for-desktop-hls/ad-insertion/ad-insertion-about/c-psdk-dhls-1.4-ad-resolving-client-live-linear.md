---
description: 라이브/선형 컨텐츠의 경우 TVSDK는 기본 스트림 컨텐츠의 청크를 동일한 기간의 광고 중단으로 대체하므로 타임라인 지속 시간이 동일하게 유지됩니다.
seo-description: 라이브/선형 컨텐츠의 경우 TVSDK는 기본 스트림 컨텐츠의 청크를 동일한 기간의 광고 중단으로 대체하므로 타임라인 지속 시간이 동일하게 유지됩니다.
seo-title: 라이브/선형 광고 삽입
title: 라이브/선형 광고 삽입
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# 라이브/선형 광고 확인 및 삽입{#live-linear-ad-resolving-and-insertion}

라이브/선형 컨텐츠의 경우 TVSDK는 기본 스트림 컨텐츠의 청크를 동일한 기간의 광고 중단으로 대체하므로 타임라인 지속 시간이 동일하게 유지됩니다.

재생 전과 재생 중에 TVSDK는 알려진 광고를 확인하고, 기본 컨텐츠의 일부를 동일한 기간의 광고 중단으로 대체하며, 필요한 경우 가상 타임라인을 재계산합니다. 광고 중단의 위치는 매니페스트에 의해 정의된 큐 포인트로 지정됩니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **컨텐츠의 시작 부분에 있는 프리롤**.
* **중간 롤로**, 컨텐츠의 중간에 있습니다.

기간이 큐 포인트 교체 기간보다 길거나 짧더라도 TVSDK에서 광고 중단이 적용됩니다. 기본적으로 TVSDK는 광고를 확인하고 배치할 때 유효한 광고 마커로 `#EXT-X-CUE` 단서를 지원합니다. 이 마커에는 메타데이터 필드 `DURATION`이(가) 초 단위이고 큐의 고유 ID가 필요합니다. 예:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>관례적인 `AdPolicySelector`을 구현할 때 `AdBreakTimelineItem`의 유형을 기반으로 하는 `AdPolicyInfo`의 프리롤, 미드롤 및 포스트롤 `AdBreakTimelineItem`s에 다른 정책을 부여할 수 있습니다.예를 들어, 중간 롤이 재생된 후에는 중간 롤의 컨텐츠를 유지할 수 있지만 재생된 후에는 프리롤 컨텐츠를 제거할 수 있습니다.

재생이 시작되면 비디오 엔진은 주기적으로 매니페스트 파일을 새로 고칩니다. TVSDK는 새 광고를 해결하고 매니페스트에 정의된 라이브 또는 선형 스트림에서 큐 포인트가 발견되면 광고를 삽입합니다. 광고가 확인되고 삽입되면 TVSDK는 가상 타임라인을 다시 계산하여 `TimelineEvent.TIMELINE_UPDATED` 이벤트를 전달합니다.
