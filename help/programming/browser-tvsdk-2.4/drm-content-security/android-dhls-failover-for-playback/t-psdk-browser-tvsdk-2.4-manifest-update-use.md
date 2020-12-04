---
description: 이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.
seo-description: 이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.
seo-title: 라이브 마스터 매니페스트 업데이트 사용
title: 라이브 마스터 매니페스트 업데이트 사용
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 라이브 마스터 매니페스트 업데이트 사용{#use-live-master-manifest-update}

이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.

1. 라이브 마스터 매니페스트 업데이트를 켜려면 `NetworkConfiguration.masterUpdateInterval` 속성을 설정하여 업데이트 빈도(분)를 설정합니다.
1. 원할 경우, `MediaPlayerItemEvent.MASTER_UPDATED` 이벤트를 수신하여 성공적인 매니페스트 업데이트를 추적합니다.
