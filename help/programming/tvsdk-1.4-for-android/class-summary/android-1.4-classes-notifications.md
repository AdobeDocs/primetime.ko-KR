---
description: 이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-description: 이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.
seo-title: 알림 클래스
title: 알림 클래스
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# 알림 클래스{#notification-classes}

이 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 수행하는 일부 활동에 대한 메시지에 대해 설명합니다.

패키지:[com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) 패키지:[com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 클래스 이름 | 설명 |
|---|---|
| MediaPlayerNotification. [오류](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 플레이어에서 재생을 중지하는 오류를 알리는 알림을 설명하는 클래스입니다. 알림 유형 ERROR의 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html)입니다. |
| MediaPlayerNotification. [정보](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 정보 알림을 설명하는 클래스입니다. 알림 유형 INFO의 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html)입니다. |
| MediaPlayerNotification. [경고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 경고 알림을 설명하는 클래스입니다. 알림 유형 WARNING의 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html)입니다. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 내에서 단일 알림 이벤트의 개체 표현을 캡슐화합니다. |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 제공된 알림 코드와 연관된 설명을 반환합니다. |
| [알림 내역](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다. 알림 이벤트 내역 목록에 대한 액세스를 제공하는 [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 개체의 순환 목록입니다. 즉, 요소 목록이 유지 관리되며, 각 요소는 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 클래스의 별도의 인스턴스를 포함합니다. ([session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 패키지에서) |
| 알림 내역을 참조하십시오. [항목](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html)의 원형 목록에 항목을 정의하고 알림과 해당 타임스탬프를 포함하는 클래스입니다. |
| MediaPlayerNotification. [응모 유형](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 지원되는 알림 유형이 포함된 클래스입니다. |