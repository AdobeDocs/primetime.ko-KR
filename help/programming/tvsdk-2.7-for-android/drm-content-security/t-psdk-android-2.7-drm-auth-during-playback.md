---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함된 경우 재생 중에 인증을 수행할 수 있습니다.
title: 재생 중 DRM 인증
exl-id: f6e6e73a-d455-4b2c-b35c-2db173372092
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 재생 중 DRM 인증 {#drm-authentication-during-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함된 경우 재생 중에 인증을 수행할 수 있습니다.

라이센스 회전으로 에셋은 여러 DRM 라이센스로 암호화됩니다. 새 DRM 메타데이터가 검색될 때마다 `DRMHelper` 메서드는 DRM 메타데이터가 DRM 인증을 요구하는지 여부를 확인하는 데 사용됩니다.

>[!TIP]
>
>재생을 시작하기 전에 도메인 바인딩 라이선스를 처리하는지 여부 및 도메인 인증이 필요한지 여부를 확인합니다. 그렇다면 도메인 인증을 완료하고 도메인에 가입하십시오.

1. 에셋에서 새 DRM 메타데이터가 검색되면 이벤트가 애플리케이션 레이어에서 발송됩니다.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. 사용 `DRMMetadata` 인증이 필요한지 여부를 확인합니다.

   * 인증이 필요하지 않은 경우 아무 작업도 수행하지 않아도 되며 재생이 중단 없이 계속됩니다.
   * 인증이 필요한 경우 DRM 인증을 완료합니다.

      이 작업은 비동기적으로 수행되며 다른 스레드에서 처리되므로 사용자 인터페이스나 비디오 재생에는 영향을 주지 않습니다.

1. 인증에 실패하면 사용자는 비디오를 계속 볼 수 없고 재생이 중지됩니다.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

예:

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
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
