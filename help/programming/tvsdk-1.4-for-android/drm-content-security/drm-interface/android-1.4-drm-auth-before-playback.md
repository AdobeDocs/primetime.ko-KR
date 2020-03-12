---
description: 비디오에 대한 DRM 메타데이터가 미디어 스트림과 분리되어 있으면 재생을 시작하기 전에 인증을 수행합니다.
seo-description: 비디오에 대한 DRM 메타데이터가 미디어 스트림과 분리되어 있으면 재생을 시작하기 전에 인증을 수행합니다.
seo-title: 재생 전 DRM 인증
title: 재생 전 DRM 인증
uuid: 326ef93d-53b0-4e3a-b16d-f3b886837cc0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 재생 전 DRM 인증 {#drm-authentication-before-playback}

비디오에 대한 DRM 메타데이터가 미디어 스트림과 분리되어 있으면 재생을 시작하기 전에 인증을 수행합니다.

비디오 자산에는 연결된 DRM 메타데이터 파일이 있을 수 있습니다. 예:

* &quot;url&quot;:&quot;<span></span>https://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;:&quot;<span></span>https://www.domain.com/asset.metadata&quot;

이 경우 `DRMHelper` 메서드를 사용하여 DRM 메타데이터 파일의 내용을 다운로드하고 분석한 다음 DRM 인증이 필요한지 확인합니다.

1. 메타데이터 URL 컨텐츠를 로드하고 다운로드한 바이트를 A로 구문 분석하는 `loadDRMMetadata` 데 `DRMMetadata`사용합니다.

   다른 네트워크 작업과 마찬가지로 이 메서드는 비동기 방식으로 자체 스레드를 만듭니다.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   예:

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. 작업은 비동기식으로 진행되므로 사용자에게 이러한 사실을 알리는 것이 좋습니다. 그렇지 않으면, 그는 왜 그의 재생이 시작되지 않는지 궁금해 할 것이다. 예를 들어 DRM 메타데이터를 다운로드하고 파싱하는 동안 스피너 휠을 표시합니다.
1. 에서 콜백을 구현합니다 `DRMLoadMetadataListener`. 이러한 이벤트 핸들러를 `loadDRMMetadata` 호출합니다(이러한 이벤트 전달).

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` 메타데이터 URL 로드가 시작된 시기를 검색합니다.
   * `onLoadMetadataUrlComplete` 메타데이터 URL의 로드가 완료된 시기를 검색합니다.
   * `onLoadMetadataUrlError` 메타데이터가 로드되지 않았음을 나타냅니다.

1. 로드가 완료되면 `DRMMetadata` 객체를 검사하여 DRM 인증이 필요한지 확인합니다.

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. 인증이 필요하지 않은 경우 재생을 시작합니다.
1. 인증이 필요한 경우 라이센스를 취득하여 인증을 수행합니다.

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

   이 예에서는 간단하게 사용자의 이름과 암호를 명시적으로 코딩합니다.

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. 이것은 네트워크 통신을 의미하므로 비동기 작업이기도 합니다. 이벤트 리스너를 사용하여 인증 상태를 확인합니다.

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. 인증이 완료되면 재생을 시작합니다.
1. 인증이 실패할 경우 사용자에게 알리고 재생을 시작하지 마십시오.

응용 프로그램에서 인증 오류를 처리해야 합니다. TVSDK를 재생하기 전에 인증에 실패하면 오류 상태가 됩니다. 즉, DRM 라이브러리의 오류 코드가 포함된 오류가 생성되고 재생이 중지됩니다. 응용 프로그램에서 문제를 해결하고 플레이어를 재설정하고 리소스를 다시 로드해야 합니다.

