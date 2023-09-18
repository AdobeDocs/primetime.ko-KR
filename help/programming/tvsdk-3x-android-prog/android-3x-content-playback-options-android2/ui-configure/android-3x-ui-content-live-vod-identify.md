---
description: 미디어 컨텐츠가 라이브 또는 VOD(Video On Demand)인지 알고 있어야 할 수 있습니다.
title: 콘텐츠가 라이브인지 VOD인지 식별
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 콘텐츠가 라이브인지 VOD인지 식별 {#identify-whether-the-content-is-live-or-vod}

미디어 컨텐츠가 라이브 또는 VOD(Video On Demand)인지 알고 있어야 할 수 있습니다.

1. 플레이어가 최소한 다음 위치에 있는지 확인합니다. `PREPARED` 주.
1. 다음을 수행할지 여부를 결정합니다. `MediaPlayerItem` 콘텐츠가 라이브임( `true`) 또는 VOD ( `false`).

   ```java
   boolean isLive();
   ```
