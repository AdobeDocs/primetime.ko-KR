---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함된 경우 재생 중에 인증을 수행합니다.
title: 재생 중 DRM 인증
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 재생 중 DRM 인증 {#drm-authentication-during-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함된 경우 재생 중에 인증을 수행합니다.

에셋이 여러 DRM 라이센스로 암호화되는 라이센스 회전 기능을 고려하십시오. 새 DRM 메타데이터가 검색될 때마다 `DRMHelper` drm 메타데이터에 DRM 인증이 필요한지 여부를 확인하는 방법입니다.

>[!NOTE]
>
>이 자습서에서는 도메인 바인딩 라이선스를 처리하지 않습니다. 가장 좋은 방법은 재생을 시작하기 전에 도메인 바인딩된 라이선스를 처리하는지 여부를 확인하는 것입니다. 해당하는 경우 도메인 인증을 수행하고(필요한 경우) 도메인에 가입합니다.

1. 에셋에서 새 DRM 메타데이터가 검색되면 이벤트가 애플리케이션 레이어에서 발송됩니다.

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

1. 사용 `DRMMetadata` 인증이 필요한지 여부를 확인합니다. 그렇지 않으면 아무 작업도 하지 마십시오. 재생이 중단되지 않고 계속됩니다.
1. 그렇지 않으면 DRM 인증을 수행합니다. 이 작업은 비동기적으로 수행되며 다른 스레드에서 처리되므로 사용자 인터페이스나 비디오 재생에는 영향을 주지 않습니다.
1. 인증에 실패하면, 사용자는 비디오 보기를 계속할 수 없고, 재생이 중단된다. 그렇지 않으면 재생이 중단되지 않고 계속됩니다.

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
