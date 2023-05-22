---
description: 이러한 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지를 설명합니다.
title: 알림 클래스
exl-id: b869c201-2731-42e5-a20e-282edd2caddc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 알림 클래스{#notification-classes}

이러한 클래스는 오류, 경고 및 TVSDK가 로깅 및 디버깅을 위해 발생하는 일부 활동에 대한 메시지를 설명합니다.

패키지: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  패키지: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 클래스 이름 | 설명 |
|---|---|
| MediaPlayerNotification. [오류](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 플레이어에서 재생을 중지시키는 오류에 대한 알림을 설명하는 클래스입니다. (이)는 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 오류 유형의 알림입니다. |
| MediaPlayerNotification. [정보](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 정보 알림을 설명하는 클래스입니다. (이)는 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 알림 유형 정보. |
| MediaPlayerNotification. [경고](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 경고 알림을 설명하는 클래스입니다. (이)는 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 경고 유형의 알림입니다. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 정보 메시지, 경고 및 오류를 제공하는 클래스입니다. 내에서 단일 알림 이벤트의 개체 표현을 캡슐화합니다. [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [알림 코드](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 제공된 알림 코드와 연관된 설명을 반환합니다. |
| [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 알림 개체의 로그를 저장하는 클래스입니다. 의 원형 목록 [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 알림 이벤트 내역 목록에 대한 액세스를 제공하는 객체입니다. 즉, 요소 목록을 유지 관리하며 각 요소는 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 클래스. (위치 [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) package.) |
| NotificationHistory. [항목](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 의 순환 목록에 있는 항목을 정의하는 클래스 [알림 기록](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 알림과 해당 타임스탬프를 보관합니다. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 지원되는 알림 유형을 포함하는 클래스입니다. |
