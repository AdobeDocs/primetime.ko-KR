---
description: MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류의 변경 내용에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.
title: 플레이어 상태, 활동, 오류 및 로깅에 대한 알림
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 개요 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류의 변경 내용에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태에도 변화를 일으킵니다.

애플리케이션은 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

이벤트 리스너를 구현하여 이벤트를 캡처하고 응답합니다. 많은 이벤트가 다음을 제공합니다 `MediaPlayerNotification` 상태 알림입니다.
