---
description: TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.
title: DRM 이벤트
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM 이벤트{#drm-events}

TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 의 구현을 등록하십시오. `MediaPlayer.DRMEventListener` 여기에는 다음 콜백이 포함됩니다.

| 이벤트 | 의미 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | 새 DRM 메타데이터를 사용할 수 있습니다. |
