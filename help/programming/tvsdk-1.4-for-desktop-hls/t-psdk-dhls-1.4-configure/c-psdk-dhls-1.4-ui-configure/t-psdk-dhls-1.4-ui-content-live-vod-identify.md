---
description: 경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.
seo-description: 경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.
seo-title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 컨텐츠가 라이브인지 VOD인지를 확인합니다.{#identify-whether-the-content-is-live-or-vod}

경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.

1. 플레이어가 INITIALIZED 상태 이상이어야 합니다.
1. 컨텐츠가 라이브인지(true), VOD(false)인지 `MediaPlayerItem` 확인합니다.

   ```
   function get isLive():Boolean;
   ```

