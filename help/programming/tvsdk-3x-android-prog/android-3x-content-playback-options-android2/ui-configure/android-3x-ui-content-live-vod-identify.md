---
description: 미디어 컨텐츠가 실시간 또는 VOD(Video On Demand)인지 알아야 할 수도 있습니다.
title: 컨텐츠가 실시간 또는 VOD인지 확인
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# 컨텐츠가 실시간 또는 VOD {#identify-whether-the-content-is-live-or-vod}인지 확인합니다.

미디어 컨텐츠가 실시간 또는 VOD(Video On Demand)인지 알아야 할 수도 있습니다.

1. 플레이어가 `PREPARED` 상태 이상이어야 합니다.
1. `MediaPlayerItem` 콘텐트가 실시간( `true`) 또는 VOD( `false`)인지 확인합니다.

   ```java
   boolean isLive();
   ```
