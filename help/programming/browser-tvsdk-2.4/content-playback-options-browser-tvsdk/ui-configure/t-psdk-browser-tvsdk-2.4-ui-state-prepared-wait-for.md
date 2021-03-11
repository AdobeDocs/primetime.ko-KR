---
description: 대부분의 브라우저 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.
title: 유효한 상태 대기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# 유효한 상태 {#wait-for-a-valid-state}을(를) 기다립니다.

대부분의 브라우저 TVSDK 플레이어 메서드를 사용하려면 먼저 플레이어가 유효한 상태여야 합니다.

그 선수는 여러 상태를 거친다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필요한 상태 이상이 아니면 많은 플레이어 메서드에서 `IllegalStateException`을(를) throw합니다.

필요한 상태는 일반적으로 COPPED입니다.

1. 상태가 준비가 되었는지 확인하려면:

   플레이어를 초기화하는 동안 브라우저 TVSDK가 `MediaPlayerStatus.PREPARED`의 `event.status`과 함께 `AdobePSDK.MediaPlayerStatusChangeEvent` 이벤트를 전달할 때까지 기다리십시오.

   MediaPlayer 객체의 현재 상태가 PREPARE 이상인지 확인합니다.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

