---
description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.
seo-description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.
seo-title: DRM 이벤트
title: DRM 이벤트
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# DRM 이벤트{#drm-events}

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 다음 콜백이 `MediaPlayer.DRMEventListener` 포함된 구현을 등록합니다.

| 이벤트 | 의미 |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo))`(DRMMetadataInfo drmMetadataInfo)` | 새로운 DRM 메타데이터를 사용할 수 있습니다. |

