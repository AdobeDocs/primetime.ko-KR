---
description: 미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.
seo-description: 미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.
seo-title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 컨텐츠가 라이브인지 VOD인지를 확인합니다. {#identify-whether-the-content-is-live-or-vod}

미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.

1. 플레이어가 적어도 `PREPARED` 상태에 있는지 확인합니다.
1. 컨텐츠가 `MediaPlayerItem` 실시간( `true``false`) 또는 VOD()인지 확인합니다.

   ```java
   boolean isLive();
   ```
