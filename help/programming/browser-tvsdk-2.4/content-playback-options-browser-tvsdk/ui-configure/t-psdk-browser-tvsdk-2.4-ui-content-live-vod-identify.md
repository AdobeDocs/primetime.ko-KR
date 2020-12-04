---
description: 미디어 컨텐츠가 실시간 또는 VOD인지 알아야 할 수도 있습니다.
seo-description: 미디어 컨텐츠가 실시간 또는 VOD인지 알아야 할 수도 있습니다.
seo-title: 컨텐츠가 실시간 또는 VOD인지 확인
title: 컨텐츠가 실시간 또는 VOD인지 확인
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 컨텐츠가 라이브인지 VOD{#identify-whether-the-content-is-live-or-vod}인지 확인합니다.

미디어 컨텐츠가 실시간 또는 VOD인지 알아야 할 수도 있습니다.

1. 브라우저 TVSDK가 `AdobePSDK.MediaPlayerStatus.PREPARED`의 `event.status`과(와) 함께 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 이벤트를 트리거할 때까지 기다립니다.

   이 단계에서는 미디어 리소스가 성공적으로 로드됩니다.

   >[!IMPORTANT]
   >
   >Browser TVSDK가 적어도 `PREPARED` 상태가 아닌 경우 다음 메서드를 호출하려고 하면 `IllegalStateException`이 발생합니다.

1. `MediaPlayerItem` 인터페이스에서 `live`을 읽습니다.

   ```js
   player.currentItem.live
   ```

