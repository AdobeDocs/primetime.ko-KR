---
description: 이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.
seo-description: 이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.
seo-title: 알림 클래스
title: 알림 클래스
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 알림 클래스{#notification-classes}

이 클래스는 TVSDK가 로깅 및 디버깅 목적으로 발생하는 오류, 경고 및 일부 활동에 대한 메시지에 대해 설명합니다.

패키지: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) 패키지: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 클래스 이름 | 설명 |
|---|---|
| MediaPlayerNotification. [오류](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 플레이어가 재생을 중지하는 오류에 대한 알림을 설명하는 클래스입니다. 알림 유형 [ERROR의](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) MediaPlayerNotification입니다. |
| MediaPlayerNotification. [정보](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 정보 알림을 설명하는 클래스입니다. 알림 유형 [INFO의](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) MediaPlayerNotification입니다. |
| MediaPlayerNotification. [경고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 경고 알림을 설명하는 클래스입니다. 알림 유형 [WARNING의](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) MediaPlayerNotification입니다. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. NotificationHistory 내에서 단일 알림 이벤트의 개체 표현을 [캡슐화합니다](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 제공된 알림 코드와 연관된 설명을 반환합니다. |
| [알림 내역](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다. 알림 이벤트 기록 [목록에 대한](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 액세스를 제공하는 NotificationHistory.Item 개체의 순환 목록입니다. 즉, 각 요소에 별도의 MediaPlayerNotification 클래스 인스턴스가 들어 있는 요소 목록이 [유지됩니다](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) . ( [세션](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 패키지에서) |
| 알림 내역을 참조하십시오. [항목](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | NotificationHistory의 원형 목록에 항목을 [정의하고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 알림과 해당 타임스탬프를 보유하는 클래스입니다. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 지원되는 알림 유형이 포함된 클래스입니다. |