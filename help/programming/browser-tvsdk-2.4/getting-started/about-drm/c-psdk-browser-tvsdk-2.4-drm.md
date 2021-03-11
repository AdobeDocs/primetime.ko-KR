---
description: Digital Rights Management(DRM) 전용 워크플로우를 완료할 수 있습니다.
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Digital Rights Management(DRM) 전용 워크플로우를 완료할 수 있습니다.

`AdobePSDK.DRMMetadataInfoEvent` 이벤트를 수신하여 DRM 워크플로우를 처리할 수 있습니다.

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Digital Rights Management {#add-digital-rights-management} 추가

1. `DRMMetadataInfoAvailableEvent`을(를) 추가하여 `DRMMetadata`을(를) 가져옵니다.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. 1단계에서 줄 위에 `onDRMMetadataInfoAvailable` 섹션을 구현합니다.

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

1. 다음 샘플을 복사하여 Widevine 및 PlayReady 보호 데이터를 만듭니다.

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