---
description: 미디어 컨텐츠가 라이브 또는 VOD(Video On Demand)인지 알고 있어야 할 수 있습니다.
title: 콘텐츠가 라이브인지 VOD인지 식별
exl-id: a75332d9-a23a-423c-8d1f-81b40ca73b21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
