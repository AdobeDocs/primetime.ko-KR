---
description: 이러한 클래스는 오류, 경고 및 로깅 및 디버깅에 문제가 되는 일부 활동에 대한 메시지를 설명합니다.
title: 알림 클래스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 알림 클래스 {#notification-classes}

이러한 클래스는 오류, 경고 및 로깅 및 디버깅에 문제가 되는 일부 활동에 대한 메시지를 설명합니다.

패키지: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 클래스 이름 | 설명 |
|---|---|
| [알림](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. 내에서 단일 알림 이벤트의 개체 표현을 캡슐화합니다. [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [알림 코드](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 제공된 알림 코드와 연관된 설명을 반환하고 알림 개체에 대한 숫자 상수를 제공합니다. |
| [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다. 의 원형 목록 [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 알림 이벤트 내역 목록에 대한 액세스를 제공하는 객체입니다. 즉, 요소 목록을 유지 관리하며 각 요소는 [알림](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) 클래스. |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 의 순환 목록에 있는 항목을 정의하는 클래스 [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) 알림과 해당 타임스탬프를 보관합니다. |
| [알림 유형](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 지원되는 알림 유형을 포함하는 클래스입니다. |
