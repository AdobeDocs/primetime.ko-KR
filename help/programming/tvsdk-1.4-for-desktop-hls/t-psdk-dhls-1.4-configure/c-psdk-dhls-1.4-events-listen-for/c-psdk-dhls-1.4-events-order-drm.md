---
description: TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 디지털 저작권 관리(DRM) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 응답하여 작업을 구현할 수 있습니다.
title: DRM 이벤트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# DRM 이벤트{#drm-events}

TVSDK는 새로운 DRM 메타데이터를 사용할 수 있는 시기 등 DRM 관련 작업에 대한 응답으로 디지털 저작권 관리(DRM) 이벤트를 전달합니다. 플레이어는 이러한 이벤트에 응답하여 작업을 구현할 수 있습니다.

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

