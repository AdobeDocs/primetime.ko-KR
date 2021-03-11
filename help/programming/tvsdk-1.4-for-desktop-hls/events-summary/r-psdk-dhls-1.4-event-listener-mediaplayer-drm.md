---
description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 디지털 저작권 관리(DRM) 이벤트를 전달합니다.
title: DRM 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# DRM 이벤트{#drm-events}

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 디지털 저작권 관리(DRM) 이벤트를 전달합니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 `MediaPlayer` 개체가 있는 DRM 이벤트에 대해 `DRMMetadataInfoEvent`을 수신합니다.

| 이벤트 | 의미 |
|---|---|
| DRMMetadataInfoEvent를 참조하십시오.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 새 DRM 메타데이터를 사용할 수 있습니다. |