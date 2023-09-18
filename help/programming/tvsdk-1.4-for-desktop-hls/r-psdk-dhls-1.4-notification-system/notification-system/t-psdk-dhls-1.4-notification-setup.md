---
description: 알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다.
title: 알림 시스템 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 알림 시스템 설정{#set-up-your-notification-system}

알림을 수신하고 고유한 알림을 알림 기록에 추가할 수 있습니다.

Primetime 플레이어 알림 시스템의 핵심은 독립 실행형 알림을 나타내는 알림 클래스입니다.

NotificationHistory 클래스는 알림을 누적하는 메커니즘을 제공합니다. 알림 로그( `NotificationHistoryItem`) 알림의 컬렉션을 나타내는 개체입니다.

알림을 받으려면:

* 알림 수신
* 알림 기록에 알림 추가

1. 상태 변경 내용을 수신합니다.
1. 구현 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 이벤트 리스너.
1. TVSDK가 `MediaPlayer.StatusChangeEvent` 인스턴스가 다음 두 매개 변수를 포함하는 이벤트 리스너에 매핑됩니다.

   * 새 상태( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` 오브젝트
