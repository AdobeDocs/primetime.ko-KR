---
description: 이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.
title: 라이브 마스터 매니페스트 업데이트 사용
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# 라이브 마스터 매니페스트 업데이트 사용{#use-live-master-manifest-update}

이 기능을 켜고 관련 이벤트를 확인할 수 있습니다.

1. 라이브 마스터 매니페스트 업데이트를 켜려면 다음을 설정하여 업데이트 빈도(분)를 설정하십시오. `NetworkConfiguration.masterUpdateInterval` 속성.
1. 필요한 경우 다음을 수신하여 성공적인 매니페스트 업데이트를 추적합니다. `MediaPlayerItemEvent.MASTER_UPDATED` 이벤트.
