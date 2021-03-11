---
description: 미디어 컨텐츠가 실시간 또는 VOD인지 알아야 할 수도 있습니다.
title: 컨텐츠가 실시간 또는 VOD인지 확인
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# 컨텐츠가 실시간 또는 VOD{#identify-whether-the-content-is-live-or-vod}인지 확인합니다.

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

