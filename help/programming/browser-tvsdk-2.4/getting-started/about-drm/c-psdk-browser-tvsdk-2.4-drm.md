---
description: Digital Rights Management(DRM)별 워크플로우를 완료할 수 있습니다.
title: Digital Rights Management
exl-id: 5a40252b-2917-4341-bc64-8642432ddda9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

Digital Rights Management(DRM)별 워크플로우를 완료할 수 있습니다.

다음 내용을 들을 수 있습니다. `AdobePSDK.DRMMetadataInfoEvent` drm 워크플로우를 처리하는 이벤트:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Digital Rights Management 추가 {#add-digital-rights-management}

1. 추가 `DRMMetadataInfoAvailableEvent` 을(를) 가져오려면 `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 구현 `onDRMMetadataInfoAvailable` 1단계에서 줄 위에 있는 섹션입니다.

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. setupVideo 메서드에서 DRMManager를 만듭니다.

   ```js
   var drmManager = player.drmManager;
   ```

1. 다음 샘플을 복사하여 Widevine 및 PlayReady에 대한 보호 데이터를 만듭니다.

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. drmManager에 보호 데이터를 추가합니다.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. 리소스 URL을 DASH 테스트 스트림으로 변경합니다.

   >[!TIP]
   >
   >이제 DASH이므로 리소스 유형을 업데이트해야 합니다.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. 구성을 테스트합니다.
