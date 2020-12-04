---
description: 이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-description: 이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-title: 알림 클래스
title: 알림 클래스
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# 알림 클래스 {#notification-classes}

이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.

| **클래스 이름** | **설명** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 플레이어에서 재생을 중지하는 오류를 알리는 알림을 설명하는 클래스입니다. 알림 유형 ERROR의 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)입니다. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Primetime Player 프레임워크에서 발송한 모든 알림을 나열합니다. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 내에 단일 알림 이벤트의 개체 표현을 캡슐화합니다. |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 알림 이벤트 기록 목록에 대한 액세스를 제공하는 알림 개체 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 개체의 로그를 저장하는 클래스입니다. 즉, 요소 목록을 유지 관리하고, 각 요소에는 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)의 별도의 인스턴스가 포함됩니다. |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)의 원형 목록에 항목을 정의하고 알림과 해당 타임스탬프를 포함하는 클래스입니다. |

