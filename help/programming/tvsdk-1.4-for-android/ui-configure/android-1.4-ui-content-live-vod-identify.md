---
description: 경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.
seo-description: 경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.
seo-title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 컨텐츠가 라이브인지 VOD인지를 확인합니다.{#identify-whether-the-content-is-live-or-vod}

경우에 따라 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 합니다.

1. 플레이어가 준비 상태 이상이어야 합니다.
1. 컨텐츠가 라이브인지(true), VOD(false)인지 `MediaPlayerItem` 확인합니다.

   ```java
   boolean isLive();
   ```

