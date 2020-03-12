---
description: 미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.
seo-description: 미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.
seo-title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 컨텐츠가 라이브인지 VOD인지를 확인합니다. {#identify-whether-the-content-is-live-or-vod}

미디어 컨텐츠가 라이브인지 VOD(Video On Demand)인지를 알고 있어야 할 수 있습니다.

1. 플레이어가 적어도 `PREPARED` 상태에 있는지 확인합니다.
1. 컨텐츠가 `MediaPlayerItem` 실시간( `true``false`) 또는 VOD()인지 확인합니다.

   ```java
   boolean isLive();
   ```
