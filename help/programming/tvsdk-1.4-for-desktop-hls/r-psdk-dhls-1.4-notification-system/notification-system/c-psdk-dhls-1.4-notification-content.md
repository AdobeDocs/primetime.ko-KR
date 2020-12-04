---
description: MediaPlayerNotification은 플레이어의 상태와 관련된 정보를 제공합니다.
seo-description: MediaPlayerNotification은 플레이어의 상태와 관련된 정보를 제공합니다.
seo-title: 알림 컨텐츠
title: 알림 컨텐츠
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 알림 내용{#notification-content}

MediaPlayerNotification은 플레이어의 상태와 관련된 정보를 제공합니다.

TVSDK는 `MediaPlayerNotification` 알림의 시간순 목록을 제공합니다. 각 알림은 다음 정보를 포함합니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * 입력 정보, 경고 또는 오류
   * `code`:알림의 숫자 표현입니다.
   * `name`:사용자가 읽을 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`:알림에 대한 관련 정보가 들어 있는 키/값 쌍입니다. 예를 들어 `URL`이라는 키는 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`:이 알림에 직접 영향을 주는 다른  `MediaPlayerNotification` 개체에 대한 참조입니다.

나중에 분석을 위해 이 정보를 로컬에 저장하거나 원격 서버에 보내 로깅 및 그래픽 표현을 할 수 있습니다.
