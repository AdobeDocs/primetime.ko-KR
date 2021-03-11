---
description: 이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.
title: 라이브 마스터 매니페스트 업데이트 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# 라이브 마스터 매니페스트 업데이트 사용{#use-live-master-manifest-update}

이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.

1. 라이브 마스터 매니페스트 업데이트를 켜려면 `NetworkConfiguration.masterUpdateInterval` 속성을 설정하여 업데이트 빈도(분)를 설정합니다.
1. 원할 경우, `MediaPlayerItemEvent.MASTER_UPDATED` 이벤트를 수신하여 성공적인 매니페스트 업데이트를 추적합니다.
