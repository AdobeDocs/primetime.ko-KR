---
description: 알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다.
title: 알림 시스템 설정
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 알림 시스템 설정{#set-up-your-notification-system}

알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다.

Primetime 플레이어 알림 시스템의 핵심은 입니다. `Notification` 클래스: 독립 실행형 알림을 나타냅니다.

다음 `NotificationHistory` 클래스는 알림을 누적하는 메커니즘을 제공합니다. 알림의 컬렉션을 나타내는 알림 로그(NotificationHistoryItem) 개체를 저장합니다.

알림을 받으려면:

* 알림 수신
* 알림 기록에 알림 추가

1. 상태 변경 내용을 수신합니다.
1. 구현 `MediaPlayer.PlaybackEventListener.onStateChanged` callback.
1. TVSDK는 두 개의 매개 변수를 콜백에 전달합니다.

   * 새 상태( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 오브젝트

