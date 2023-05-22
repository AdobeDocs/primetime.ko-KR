---
description: 미디어 콘텐츠가 라이브인지 VOD인지 알고 있어야 하는 경우가 있습니다.
title: 콘텐츠가 라이브인지 VOD인지 식별
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 콘텐츠가 라이브인지 VOD인지 식별{#identify-whether-the-content-is-live-or-vod}

미디어 콘텐츠가 라이브인지 VOD인지 알고 있어야 하는 경우가 있습니다.

1. 플레이어가 적어도 PREPARED 상태에 있는지 확인합니다.
1. 다음을 수행할지 여부를 결정합니다. `MediaPlayerItem` 콘텐츠는 라이브(true) 또는 VOD(false)입니다.

   ```java
   boolean isLive();
   ```
