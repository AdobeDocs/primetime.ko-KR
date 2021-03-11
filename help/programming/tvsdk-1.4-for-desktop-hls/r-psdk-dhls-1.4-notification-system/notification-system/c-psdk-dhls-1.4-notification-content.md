---
description: MediaPlayerNotification은 플레이어의 상태와 관련된 정보를 제공합니다.
title: 알림 내용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 알림 내용{#notification-content}

MediaPlayerNotification은 플레이어의 상태와 관련된 정보를 제공합니다.

TVSDK는 `MediaPlayerNotification` 알림의 시간순 목록을 제공합니다. 각 알림에는 다음 정보가 포함됩니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * 정보 입력, 경고 또는 오류
   * `code`:알림의 숫자 표현입니다.
   * `name`:SEEK_ERROR와 같이 사용자가 읽을 수 있는 알림 설명
   * `metadata`:알림에 대한 관련 정보가 들어 있는 키/값 쌍. 예를 들어 `URL` 키는 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`:이 알림에 직접 영향을 주는 다른  `MediaPlayerNotification` 개체에 대한 참조입니다.

나중에 분석을 위해 이 정보를 로컬에 저장하거나 원격 서버에 보내 로깅과 그래픽 표현을 할 수 있습니다.
