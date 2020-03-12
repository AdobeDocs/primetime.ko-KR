---
description: MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태도 변경됩니다.
seo-description: MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태도 변경됩니다.
seo-title: 플레이어 상태, 활동, 오류 및 로깅에 대한 알림
title: 플레이어 상태, 활동, 오류 및 로깅에 대한 알림
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 개요 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification 개체는 플레이어 상태, 경고 및 오류 변화에 대한 정보를 제공합니다. 비디오 재생을 중지하는 오류는 플레이어의 상태도 변경됩니다.

응용 프로그램은 알림 및 상태 정보를 검색할 수 있습니다. 알림 정보를 사용하여 진단 및 유효성 검사를 위한 로깅 시스템을 만들 수도 있습니다.

이벤트 리스너를 구현하여 이벤트를 캡처하고 응답합니다. 많은 이벤트가 `MediaPlayerNotification` 상태 알림을 제공합니다.