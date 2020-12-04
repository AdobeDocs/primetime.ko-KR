---
description: '이제 com.adobe.mediacore.timeline.TimelineMarker 인터페이스에 새 메서드가 포함되어 있습니다. '
seo-description: '이제 com.adobe.mediacore.timeline.TimelineMarker 인터페이스에 새 메서드가 포함되어 있습니다. '
seo-title: '2.5.x 레이지 광고 해결에서 3.0.0 레이지 광고 해결(API/워크플로우 변경)으로 업그레이드 '
title: '2.5.x 레이지 광고 해결에서 3.0.0 레이지 광고 해결(API/워크플로우 변경)으로 업그레이드 '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# 2.5.x 레이지 광고 해결에서 3.x 레이지 광고 해결(API/워크플로우 변경):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

이제 com.adobe.mediacore.timeline.TimelineMarker 인터페이스에 새 메서드가 포함되어 있습니다.

**Placement.Type getPlacementType()**

이 메서드는 Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL 또는 Placement.Type.POST_ROLL의 배치 유형을 반환합니다. 광고 나누기가 해결되지 않으면 TimelineMarker 인터페이스의 `getDuration()`메서드가 0을 반환합니다.

>[!NOTE]
>
>아직 해결되지 않은 경우 이 인터페이스가 com.mediacore.timeline.advertising.AdBreakTimelineItem 형식으로 항상 표시되는 것은 아닙니다. TimelineMarker의 `getDuration()` 메서드가 0보다 큰 경우 캐스트할 수 있습니다.

**이벤트 변경 사항:**

`kEventAdResolutionComplete` 가 이제 감가 상각되어 플레이어가 준비 상태로 들어간 직후 트리거됩니다. 이전에 이 이벤트만 듣고 스크러빙 막대만 그린 응용 프로그램은 `kEventTimelineUpdated`만 수신하도록 이 설정을 변경해야 합니다. 개별 광고 중단이 해결되면 새 `kEventTimelineUpdated` 이벤트가 전달됩니다.
