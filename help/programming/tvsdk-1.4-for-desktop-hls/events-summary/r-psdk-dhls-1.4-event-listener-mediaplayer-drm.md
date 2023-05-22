---
description: TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.
title: DRM 이벤트
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM 이벤트{#drm-events}

TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 다음을 들어보십시오. `DRMMetadataInfoEvent` 를 사용하는 DRM 이벤트용 `MediaPlayer` 개체.

| 이벤트 | 의미 |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 새 DRM 메타데이터를 사용할 수 있습니다. |
