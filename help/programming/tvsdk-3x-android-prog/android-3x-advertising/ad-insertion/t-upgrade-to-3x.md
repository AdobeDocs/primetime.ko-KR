---
description: 이제 com.adobe.mediacore.timeline.TimelineMarker 인터페이스에는 새 메서드가 포함됩니다
title: 2.5.x 레이지 광고 해결에서 3.0.0 레이지 광고 해결로 업그레이드(API/워크플로우 변경)
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 2.5.x 지연 광고 해결에서 3.x 지연 광고 해결로 업그레이드(API/워크플로우 변경):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

이제 com.adobe.mediacore.timeline.TimelineMarker 인터페이스에는 새로운 메서드가 포함됩니다.

**Placement.Type getPlacementType()**

이 메서드는 Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL 또는 Placement.Type.Placement_ROLL의 POST 유형을 반환합니다. 광고 브레이크가 해결되지 않으면 `getDuration()`timelineMarker 인터페이스의 메서드는 0을 반환합니다.

>[!NOTE]
>
>아직 해결되지 않은 경우 이 인터페이스가 항상 com.mediacore.timeline.advertising.AdBreakTimelineItem 형식으로 변환되지는 않습니다. 이 경우 캐스팅할 수 있습니다. `getDuration()` timelineMarker의 메서드가 0보다 큽니다.

**이벤트 변경 사항:**

`kEventAdResolutionComplete` 는 이제 더 이상 사용되지 않으며, 이제 플레이어가 PREPARED 상태에 들어간 직후에 트리거됩니다. 이전에 스크러빙 막대를 그리기 위해 이 이벤트만 들었던 응용 프로그램은 듣도록 이 이벤트를 변경해야 합니다. `kEventTimelineUpdated` 만 해당. 개별 광고 브레이크가 해결되면 `kEventTimelineUpdated` 이벤트가 발송됩니다.
