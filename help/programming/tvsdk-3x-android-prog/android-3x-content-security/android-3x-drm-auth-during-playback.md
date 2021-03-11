---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함되어 있으면 재생 중에 인증을 수행할 수 있습니다.
title: 재생 중 DRM 인증
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 재생 중 DRM 인증 {#drm-authentication-during-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림에 포함되어 있으면 재생 중에 인증을 수행할 수 있습니다.

라이선스 회전을 통해 에셋은 여러 DRM 라이선스를 통해 암호화됩니다. 새 DRM 메타데이터가 검색될 때마다 DRM 메타데이터에 DRM 인증이 필요한지 여부를 확인하는 데 `DRMHelper` 메서드가 사용됩니다.

>[!TIP]
>
>재생을 시작하기 전에 도메인 바인딩된 라이선스를 처리하는지 여부와 도메인 인증이 필요한지 여부를 결정합니다. 예: 도메인 인증을 완료하고 도메인에 가입하십시오.

1. 새로운 DRM 메타데이터가 자산에서 검색되면 응용 프로그램 레이어에 이벤트가 전달됩니다.

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

1. 인증이 필요한지 여부를 확인하려면 `DRMMetadata`을 사용합니다.

   * 인증이 필요하지 않은 경우 아무 작업도 수행할 필요가 없으며 계속 재생할 수 있습니다.
   * 인증이 필요한 경우 DRM 인증을 완료하십시오.

      이 작업은 비동기적이며 다른 스레드에서 처리되므로 사용자 인터페이스나 비디오 재생에 영향을 주지 않습니다.

1. 인증이 실패하면 사용자가 비디오를 계속 볼 수 없으며 재생이 중지됩니다.

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
