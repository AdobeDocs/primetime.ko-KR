---
description: 이러한 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지를 설명합니다.
title: 알림 클래스
exl-id: 611a886b-a77a-4092-ab05-25e496fec8b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 알림 클래스{#notification-classes}

이러한 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지를 설명합니다.

| 클래스 이름 | 설명 |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 플레이어에서 재생을 중지시키는 오류에 대한 알림을 설명하는 클래스입니다. (이)는 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) 오류 유형의 알림입니다. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Primetime 플레이어 프레임워크에서 발송한 모든 알림을 나열합니다. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. 내에서 단일 알림 이벤트의 개체 표현을 캡슐화합니다. [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 알림 이벤트 내역 목록에 대한 액세스를 제공하는 객체입니다. 즉, 요소 목록을 유지 관리하며 각 요소는 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 의 순환 목록에 있는 항목을 정의하는 클래스 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 알림과 해당 타임스탬프를 보관합니다. |
