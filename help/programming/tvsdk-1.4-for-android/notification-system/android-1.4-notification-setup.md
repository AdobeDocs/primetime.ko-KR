---
description: 알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.
seo-description: 알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.
seo-title: 알림 시스템 설정
title: 알림 시스템 설정
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 알림 시스템 설정{#set-up-your-notification-system}

알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.

Primetime Player 알림 시스템의 핵심은 `Notification` 클래스입니다. 이는 독립 실행형 알림을 나타냅니다.

이 `NotificationHistory` 클래스는 알림을 축적하는 메커니즘을 제공합니다. 알림 컬렉션을 나타내는 알림 로그(NotificationHistoryItem) 개체를 저장합니다.

알림을 받으려면:

* 알림 수신
* 알림 내역에 알림 추가

1. 상태 변화에 대한 의견 수렴
1. 콜백을 `MediaPlayer.PlaybackEventListener.onStateChanged` 구현합니다.
1. TVSDK는 콜백으로 두 개의 매개 변수를 전달합니다.

   * 새 상태( `MediaPlayer.PlayerState`)
   * 개체 `MediaPlayerNotification`

