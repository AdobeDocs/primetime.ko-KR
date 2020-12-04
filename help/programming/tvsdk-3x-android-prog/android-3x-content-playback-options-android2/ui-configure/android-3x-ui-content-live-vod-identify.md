---
description: 미디어 컨텐츠가 실시간 또는 VOD(Video On Demand)인지 알고 있어야 할 수도 있습니다.
seo-description: 미디어 컨텐츠가 실시간 또는 VOD(Video On Demand)인지 알고 있어야 할 수도 있습니다.
seo-title: 컨텐츠가 실시간 또는 VOD인지 확인
title: 컨텐츠가 실시간 또는 VOD인지 확인
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 컨텐츠가 라이브 또는 VOD {#identify-whether-the-content-is-live-or-vod}인지 확인합니다.

미디어 컨텐츠가 실시간 또는 VOD(Video On Demand)인지 알고 있어야 할 수도 있습니다.

1. 플레이어가 `PREPARED` 상태 이상이어야 합니다.
1. `MediaPlayerItem` 콘텐츠가 라이브( `true`) 또는 VOD( `false`)인지 확인합니다.

   ```java
   boolean isLive();
   ```
