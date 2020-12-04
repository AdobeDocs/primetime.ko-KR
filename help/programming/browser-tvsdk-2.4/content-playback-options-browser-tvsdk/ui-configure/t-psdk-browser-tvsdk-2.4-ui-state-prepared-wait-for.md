---
description: 대부분의 Browser TVSDK 플레이어 메서드를 사용하려면 플레이어가 유효한 상태여야 합니다.
seo-description: 대부분의 Browser TVSDK 플레이어 메서드를 사용하려면 플레이어가 유효한 상태여야 합니다.
seo-title: 유효한 상태 대기
title: 유효한 상태 대기
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 유효한 상태 {#wait-for-a-valid-state}을(를) 기다리는 중

대부분의 Browser TVSDK 플레이어 메서드를 사용하려면 플레이어가 유효한 상태여야 합니다.

그 선수는 여러 주를 거친다. 플레이어가 올바른 상태를 유지할 때까지 기다리면 미디어 리소스가 성공적으로 로드됩니다. 플레이어가 필수 상태가 아닌 경우 많은 플레이어 메서드에서 `IllegalStateException`을(를) throw합니다.

필요한 상태는 일반적으로 COPIED입니다.

1. 상태가 PREMITED인지 확인하려면:

   플레이어를 초기화하는 동안 브라우저 TVSDK가 `event.status`/`MediaPlayerStatus.PREPARED`의 &lt;a1/>와 함께 `AdobePSDK.MediaPlayerStatusChangeEvent` 이벤트를 전달할 때까지 기다리십시오.

   MediaPlayer 개체의 현재 상태가 PREMITED 이상인지 확인합니다.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

