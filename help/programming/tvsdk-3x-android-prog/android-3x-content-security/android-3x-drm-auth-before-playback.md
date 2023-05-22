---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림과 별개인 경우 재생을 시작하기 전에 인증해야 합니다.
title: 재생 전 DRM 인증
exl-id: 74eb7218-403e-4264-9063-bf959403436f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 재생 전 DRM 인증 {#drm-authentication-before-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림과 별개인 경우 재생을 시작하기 전에 인증해야 합니다.

비디오 에셋에는 다음과 같은 연관된 DRM 메타데이터 파일이 있을 수 있습니다.

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

이 예에서 `DRMHelper` DRM 메타데이터 파일의 컨텐츠를 다운로드하고 구문 분석한 다음 DRM 인증이 필요한지 여부를 확인하는 방법입니다.

1. 사용 `loadDRMMetadata` 메타데이터 URL 콘텐츠를 로드하고 다운로드한 바이트를 로 구문 분석하려면 `DRMMetadata`.

   >[!TIP]
   >
   >이 메서드는 비동기적으로 수행되며 자체 스레드를 만듭니다.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   예:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. 이 작업은 비동기적임을 사용자에게 알립니다. 사용자에게 이를 알리는 것이 좋습니다.

   사용자가 이 작업이 비동기라는 것을 모를 경우 재생이 아직 시작되지 않은 이유를 궁금해할 수 있습니다. 예를 들어 DRM 메타데이터를 다운로드하고 구문 분석하는 동안 회전 휠을 표시할 수 있습니다.

1. 에서 콜백 구현 `DRMLoadMetadataListener`.

   다음 `loadDRMMetadata` 는 이러한 이벤트 처리기를 호출합니다.

   ```java
   public interface DRMLoadMetadataListener { 
   
       public void onLoadMetadataUrlStart(); 
   
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   ```

   핸들러에 대한 추가 세부 정보는 다음과 같습니다.

   * `onLoadMetadataUrlStart` 은 메타데이터 URL 로드가 시작된 시기를 감지합니다.
   * `onLoadMetadataUrlComplete` 은 메타데이터 URL 로드가 완료되면 를 검색합니다.
   * `onLoadMetadataUrlError` 는 메타데이터를 로드하지 못했음을 나타냅니다.

1. 로드가 완료되면 다음을 검사합니다. `DRMMetadata` DRM 인증이 필요한지 여부를 결정하는 개체입니다.

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   예:

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. 다음 작업 중 하나를 완료하십시오.

   * 인증이 필요하지 않으면 재생을 시작합니다.
   * 인증이 필요한 경우 라이센스를 획득하여 인증을 완료하십시오.

      ```java
      /** 
      * Helper method to perform DRM authentication. 
      * 
      * @param drmManager 
      * the DRMManager, used to perform the authentication. 
      * @param drmMetadata 
      * the DRMMetadata, containing the DRM specific information. 
      * @param authenticationListener 
      * the listener, on which the user can be notified about the 
      * authentication process status. 
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      이 예에서는 간소화를 위해 사용자의 이름과 암호를 명시적으로 코딩했습니다.

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. 이벤트 리스너를 사용하여 인증 상태를 확인합니다.

   이 프로세스는 네트워크 통신을 의미하므로 이 또한 비동기 작업입니다.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. 인증이 성공하면 재생을 시작합니다.
1. 인증이 성공하지 않으면 사용자에게 알리고 재생을 시작하지 마십시오.

   응용 프로그램에서 모든 인증 오류를 처리해야 합니다. 재생하기 전에 인증하지 못하면 TVSDK가 오류 상태에 놓이고 재생이 중지됩니다. 응용 프로그램에서 문제를 해결하고 플레이어를 재설정한 다음 리소스를 다시 로드해야 합니다.
