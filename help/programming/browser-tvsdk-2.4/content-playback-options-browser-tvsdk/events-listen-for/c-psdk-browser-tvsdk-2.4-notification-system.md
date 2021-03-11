---
description: Browser TVSDK 라이브러리의 알림 부분은 진단 및 유효성 검사 목적으로 유용한 로깅 및 디버깅 시스템을 만들 수 있도록 해줍니다.
title: 알림 시스템
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 알림 시스템 {#notification-system}

Browser TVSDK 라이브러리의 알림 부분은 진단 및 유효성 검사 목적으로 유용한 로깅 및 디버깅 시스템을 만들 수 있도록 해줍니다.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

브라우저 TVSDK에는 해당 API에 대한 *throw* 정책이 없습니다. 대부분의 메서드는 `PSDKErrorCode` 값을 반환하여 메서드가 성공적으로 실행되었는지 여부를 나타냅니다. 가능한 모든 `PSDKErrorCode` 값의 전체 목록은 브라우저 TVSDK API 참조를 참조하십시오.

비동기 오류는 특정 이벤트를 통해 알립니다.

브라우저 TVSDK는 플레이어 활동에 대한 정보를 제공하기 위해 `MediaPlayer` 이벤트를 전달합니다. 이러한 이벤트를 캡처하고 응답하려면 이벤트 리스너를 구현해야 합니다.

>[!TIP]
>
>주요 이벤트와 정보는 웹 브라우저 콘솔에 기록됩니다.

## 알림 수신 {#section_06B96633433D497E842FB7ADD5F2C7DA}

알림을 수신하고 자신만의 알림을 알림 내역에 추가할 수 있습니다. 브라우저 TVSDK 알림 시스템의 핵심은 `Notification` 클래스로, 독립 실행형 알림을 나타냅니다.

응용 프로그램이 알림을 수신하도록 설정하려면 다음을 수행하십시오.

1. MediaPlayer 인스턴스를 사용하여 MediaPlayer 상태 변경 사항을 수신합니다.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 콜백을 구현합니다.

   콜백은 `AdobePSDK.MediaPlayerStatusChangeEvent` 인스턴스를 수신하며, 브라우저 TVSDK는 이 이벤트 객체를 새 플레이어 상태가 포함된 콜백으로 전달합니다.
1. 응용 프로그램은 `MediaPlayer` 인스턴스를 사용하여 브라우저 TVSDK에서 전달하는 다른 이벤트를 수신할 수 있습니다.

