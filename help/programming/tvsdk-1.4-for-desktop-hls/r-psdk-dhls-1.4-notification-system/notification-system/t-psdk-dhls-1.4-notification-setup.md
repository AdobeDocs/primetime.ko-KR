---
description: 알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.
seo-description: 알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.
seo-title: 알림 시스템 설정
title: 알림 시스템 설정
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 알림 시스템 설정{#set-up-your-notification-system}

알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.

Primetime Player 알림 시스템의 핵심은 Notification 클래스입니다. 이는 독립 실행형 알림을 나타냅니다.

NotificationHistory 클래스는 알림을 축적하는 메커니즘을 제공합니다. 알림 컬렉션을 나타내는 알림( `NotificationHistoryItem`) 개체의 로그를 저장합니다.

알림을 받으려면:

* 알림 수신
* 알림 내역에 알림 추가

1. 상태 변화에 대한 의견 수렴
1. 이벤트 리스너를 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 구현합니다.
1. TVSDK는 다음 두 가지 매개 변수를 포함하는 이벤트 리스너에 `MediaPlayer.StatusChangeEvent` 인스턴스를 전달합니다.

   * 새 상태( `MediaPlayer.Status`)
   * 개체 `MediaPlayerNotification`

