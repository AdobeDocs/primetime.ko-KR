---
description: 이러한 클래스는 오류, 경고 및 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-description: 이러한 클래스는 오류, 경고 및 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-title: 알림 클래스
title: 알림 클래스
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 알림 클래스 {#notification-classes}

이러한 클래스는 오류, 경고 및 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지에 대해 설명합니다.

패키지: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 클래스 이름 | 설명 |
|---|---|
| [알림](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. NotificationHistory 내에서 단일 알림 이벤트의 개체 표현을 [캡슐화합니다](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 제공된 알림 코드와 연관된 설명을 반환하고 알림 객체에 대한 숫자 상수를 제공합니다. |
| [알림 내역](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다. 알림 이벤트 기록 [목록에 대한](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 액세스를 제공하는 NotificationHistoryItem 개체의 순환 목록입니다. 즉, 각 요소에 별도의 Notification 클래스 인스턴스가 들어 있는 요소 목록을 유지 [관리합니다](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) . |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | NotificationHistory의 원형 목록에 항목을 [정의하고](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) 알림과 해당 타임스탬프를 보유하는 클래스입니다. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 지원되는 알림 유형이 포함된 클래스입니다. |

