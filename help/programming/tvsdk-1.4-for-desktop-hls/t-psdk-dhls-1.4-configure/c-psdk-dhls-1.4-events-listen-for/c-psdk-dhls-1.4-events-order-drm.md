---
description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 동작을 구현할 수 있습니다.
seo-description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 동작을 구현할 수 있습니다.
seo-title: DRM 이벤트
title: DRM 이벤트
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# DRM 이벤트{#drm-events}

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 동작을 구현할 수 있습니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 다음을 수신하십시오.

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

다음 예는 일반적인 진행 상태를 보여줍니다.

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

