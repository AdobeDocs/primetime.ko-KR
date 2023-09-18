---
description: TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 작업을 구현할 수 있습니다.
title: DRM 이벤트
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# DRM 이벤트{#drm-events}

TVSDK는 새 DRM 메타데이터를 사용할 수 있게 되는 등의 DRM 관련 작업에 대한 응답으로 DRM(디지털 권한 관리) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 대한 응답으로 작업을 구현할 수 있습니다.

모든 DRM 관련 이벤트에 대한 알림을 받으려면 다음을 확인하십시오.

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

다음 예는 일반적인 진행률을 보여 줍니다.

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
