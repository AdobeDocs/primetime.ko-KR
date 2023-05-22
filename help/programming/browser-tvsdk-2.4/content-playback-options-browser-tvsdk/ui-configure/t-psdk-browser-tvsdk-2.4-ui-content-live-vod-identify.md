---
description: 미디어 콘텐츠가 라이브인지 VOD인지 알아야 할 수 있습니다.
title: 콘텐츠가 라이브인지 VOD인지 식별
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 콘텐츠가 라이브인지 VOD인지 식별{#identify-whether-the-content-is-live-or-vod}

미디어 콘텐츠가 라이브인지 VOD인지 알아야 할 수 있습니다.

1. 브라우저 TVSDK가 다음을 트리거할 때까지 대기 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 이 있는 이벤트 `event.status` / `AdobePSDK.MediaPlayerStatus.PREPARED`.

   이 단계에서는 미디어 리소스가 성공적으로 로드되었는지 확인합니다.

   >[!IMPORTANT]
   >
   >브라우저 TVSDK가 적어도 다음 범위에 있지 않은 경우 `PREPARED` state, 다음 메서드를 호출하려고 하면 `IllegalStateException`.

1. 읽기 `live` 다음에서 `MediaPlayerItem` 인터페이스:

   ```js
   player.currentItem.live
   ```
