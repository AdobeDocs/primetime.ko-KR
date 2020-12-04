---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함되면 재생하는 동안 인증을 수행합니다.
seo-description: 비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함되면 재생하는 동안 인증을 수행합니다.
seo-title: 재생 중 DRM 인증
title: 재생 중 DRM 인증
uuid: a1a63e3e-be34-49e1-96c4-ae266003b3d1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 재생 중 DRM 인증 {#drm-authentication-during-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함되면 재생하는 동안 인증을 수행합니다.

여러 DRM 라이선스를 통해 에셋이 암호화되는 라이선스 순환 기능을 고려해 보십시오. 새 DRM 메타데이터가 검색될 때마다 `DRMHelper` 메서드를 사용하여 DRM 메타데이터에 DRM 인증이 필요한지 확인합니다.

>[!NOTE]
>
>이 자습서에서는 도메인 바인딩된 라이선스를 처리하지 않습니다. 재생을 시작하기 전에 도메인 바인딩된 라이선스를 사용하고 있는지 여부를 확인하는 것이 좋습니다. 예: 도메인 인증을 수행하고(필요한 경우) 도메인에 가입합니다.

1. 새로운 DRM 메타데이터가 자산에서 검색되면 응용 프로그램 레이어에 이벤트가 전달됩니다.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. 인증 필요 여부를 확인하려면 `DRMMetadata`을 사용하십시오. 그렇지 않으면 아무 것도 하지 마십시오.재생이 중단되지 않습니다.
1. 그렇지 않으면 DRM 인증을 수행합니다. 이 작업은 비동기 작업이며 다른 스레드에서 처리되므로 사용자 인터페이스나 비디오 재생에 영향을 주지 않습니다.
1. 인증이 실패하면 사용자가 비디오를 계속 볼 수 없으며 재생이 중지됩니다. 그렇지 않으면 재생을 중단하지 않고 계속 수행할 수 있습니다.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
        }); 
    } 
};
```
