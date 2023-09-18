---
description: MediaPlayerNotification은 플레이어 상태와 관련된 정보를 제공합니다.
title: 알림 콘텐츠
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 알림 콘텐츠{#notification-content}

MediaPlayerNotification은 플레이어 상태와 관련된 정보를 제공합니다.

TVSDK는 의 시간 순 목록을 제공합니다. `MediaPlayerNotification` 알림입니다. 각 알림에는 다음 정보가 포함됩니다.

* 타임스탬프
* 다음 요소로 구성된 진단 메타데이터:

   * 유형 정보, 경고 또는 오류
   * `code`: 알림의 숫자 표현입니다.
   * `name`: 사람이 인식할 수 있는 알림 설명(예: SEEK_ERROR)
   * `metadata`: 알림에 대한 관련 정보가 포함된 키/값 쌍. 예를 들어 `URL` 알림과 관련된 URL인 값을 제공합니다.

   * `innerNotification`: 다른 참조에 대한 참조 `MediaPlayerNotification` 이 알림에 직접 영향을 주는 개체입니다.

나중에 분석할 수 있도록 이 정보를 로컬에 저장하거나 로깅 및 그래픽 표시를 위해 원격 서버로 전송할 수 있습니다.
