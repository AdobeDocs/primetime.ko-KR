---
description: 알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.
title: 알림 시스템 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 알림 시스템 설정{#set-up-your-notification-system}

알림을 수신할 수 있으며 자신만의 알림을 알림 내역에 추가할 수 있습니다.

Primetime 플레이어 알림 시스템의 핵심은 독립형 알림을 나타내는 `Notification` 클래스입니다.

`NotificationHistory` 클래스는 알림을 축적하는 메커니즘을 제공합니다. 알림 컬렉션을 나타내는 알림 로그(NotificationHistoryItem) 개체를 저장합니다.

알림을 받으려면:

* 알림 수신
* 알림 내역에 알림 추가

1. 상태 변경 사항을 수신합니다.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 콜백을 구현합니다.
1. TVSDK는 콜백에 2개의 매개 변수를 전달합니다.

   * 새 상태( `MediaPlayer.PlayerState`)
   * `MediaPlayerNotification` 개체

