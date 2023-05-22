---
description: 브라우저 TVSDK 라이브러리의 알림 부분을 사용하면 진단 및 유효성 검사 목적으로 유용할 수 있는 로깅 및 디버깅 시스템을 만들 수 있습니다.
title: 알림 시스템
exl-id: 6a3a3c56-1580-4f43-ba81-220a5b0fe5c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 알림 시스템 {#notification-system}

브라우저 TVSDK 라이브러리의 알림 부분을 사용하면 진단 및 유효성 검사 목적으로 유용할 수 있는 로깅 및 디버깅 시스템을 만들 수 있습니다.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

브라우저 TVSDK에 *no throw* API에 대한 정책. 대부분의 메서드는 `PSDKErrorCode` 메서드가 성공적으로 실행되었는지 여부를 나타내는 값입니다. 가능한 모든 것의 전체 목록을 위해 `PSDKErrorCode` 값은 브라우저 TVSDK API 참조 를 참조하십시오.

비동기 오류는 특정 이벤트를 통해 통지됩니다.

브라우저 TVSDK 디스패치 `MediaPlayer` 플레이어 활동에 대한 정보를 제공하는 이벤트입니다. 이러한 이벤트를 캡처하고 응답하려면 이벤트 리스너를 구현해야 합니다.

>[!TIP]
>
>주요 이벤트 및 정보는 웹 브라우저 콘솔에 기록됩니다.

## 알림 수신 {#section_06B96633433D497E842FB7ADD5F2C7DA}

알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다. 브라우저 TVSDK 알림 시스템의 핵심은 입니다. `Notification` 클래스: 독립 실행형 알림을 나타냅니다.

알림을 수신하도록 애플리케이션을 설정하려면 다음을 수행하십시오.

1. MediaPlayer 인스턴스를 사용하여 MediaPlayer 상태 변경 사항을 수신합니다.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 콜백을 구현합니다.

   콜백은 `AdobePSDK.MediaPlayerStatusChangeEvent`, 그리고 브라우저 TVSDK가 이 이벤트 개체를 새 플레이어 상태가 포함된 콜백에 전달합니다.
1. 응용 프로그램은 다음을 사용하여 브라우저 TVSDK에서 발송하는 다른 이벤트를 수신할 수 있습니다. `MediaPlayer` 인스턴스.
