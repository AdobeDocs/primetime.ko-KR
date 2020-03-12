---
description: 이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.
seo-description: 이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.
seo-title: 알림 클래스
title: 알림 클래스
uuid: 08c29efe-245d-4a6d-80c6-cd561cbf3b5f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 알림 클래스{#notification-classes}

이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.

| 클래스 이름 | 설명 |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 플레이어가 재생을 중지하는 오류에 대한 알림을 설명하는 클래스입니다. 알림 유형 [ERROR의](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) PTNotification입니다. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Primetime Player 프레임워크에서 전달한 모든 알림을 나열합니다. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. PTNotificationHistory 내에서 단일 알림 이벤트의 개체 표현을 [캡슐화합니다](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 알림 이벤트 내역 목록에 대한 액세스를 제공하는 알림 개체 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 개체의 로그를 저장하는 클래스입니다. 즉, 요소 목록을 유지 관리하고 각 요소에 별도의 PTNotification 인스턴스를 [포함합니다](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | PTNotificationHistory의 원형 목록에 항목을 [정의하고](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 알림과 해당 타임스탬프를 보유하는 클래스입니다. |

