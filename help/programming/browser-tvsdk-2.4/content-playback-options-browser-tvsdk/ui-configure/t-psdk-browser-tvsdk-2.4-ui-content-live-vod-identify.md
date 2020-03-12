---
description: 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 할 수 있습니다.
seo-description: 미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 할 수 있습니다.
seo-title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
title: 컨텐츠가 라이브인지 VOD인지를 확인합니다.
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 컨텐츠가 라이브인지 VOD인지를 확인합니다.{#identify-whether-the-content-is-live-or-vod}

미디어 컨텐츠가 라이브인지 VOD인지를 알고 있어야 할 수 있습니다.

1. 브라우저 TV SDK가 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 이벤트를 트리거할 `event.status` 때까지 기다립니다 `AdobePSDK.MediaPlayerStatus.PREPARED`.

   이 단계에서는 미디어 리소스가 성공적으로 로드됩니다.

   >[!IMPORTANT]
   >
   >Browser TVSDK가 적어도 `PREPARED` 상태에 있지 않으면 다음 메서드를 호출하려고 하면 오류가 발생합니다 `IllegalStateException`.

1. 다음 `live` `MediaPlayerItem` 인터페이스에서 읽기:

   ```js
   player.currentItem.live
   ```

