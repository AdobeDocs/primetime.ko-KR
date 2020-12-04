---
description: TVSDK는 새로운 DRM 메타데이터가 사용 가능한 시기 등 DRM 관련 작업에 응답하여 디지털 저작권 관리(DRM) 이벤트를 전달합니다.
seo-description: TVSDK는 새로운 DRM 메타데이터가 사용 가능한 시기 등 DRM 관련 작업에 응답하여 디지털 저작권 관리(DRM) 이벤트를 전달합니다.
seo-title: DRM 이벤트
title: DRM 이벤트
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# DRM 이벤트{#drm-events}

TVSDK는 새로운 DRM 메타데이터가 사용 가능한 시기 등 DRM 관련 작업에 응답하여 디지털 저작권 관리(DRM) 이벤트를 전달합니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 `MediaPlayer` 개체가 있는 DRM 이벤트에 대해 `DRMMetadataInfoEvent`을 수신하십시오.

| 이벤트 | 의미 |
|---|---|
| DRMMetadataInfoEvent를 참조하십시오.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | 새로운 DRM 메타데이터를 사용할 수 있습니다. |