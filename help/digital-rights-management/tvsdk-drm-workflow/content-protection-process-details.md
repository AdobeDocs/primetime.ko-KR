---
seo-title: 라이센스 획득 프로세스 세부 정보
title: 라이센스 획득 프로세스 세부 정보
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# 라이센스 획득 프로세스 세부 정보 {#license-acquisition-process-details}

Primetime DRM으로 보호된 콘텐츠 워크플로우에 대한 API 수준의 세부 보기를 제공합니다.

1. `URLLoader` 개체를 사용하여 보호된 콘텐츠의 메타데이터 파일의 바이트를 로드합니다.

   이 개체를 `metadata_bytes`과 같은 변수로 설정합니다. Primetime DRM으로 제어되는 모든 콘텐츠에는 Primetime DRM 메타데이터가 있습니다. 컨텐츠가 패키지되면 이 메타데이터를 컨텐츠와 함께 별도의 메타데이터 파일( [!DNL .metadata])로 저장할 수 있습니다. 또는 메타데이터를 Base64로 인코딩하여 비디오 매니페스트 파일 본문에 삽입할 수 있습니다. 자세한 내용은 [미디어 파일 패키징](../protecting-content/packaging-media-overview/packaging-media-files.md)을 참조하십시오.
   1. 필요한 경우 문자열 시작 위치에서 느낌표 `!`를 제거합니다.
   1. HLS 또는 HDS 컨텐츠에 필요한 경우 Base64로 인코딩된 문자열에 포함된 메타데이터를 이진 데이터로 디코딩하고 전달하십시오.
1. `DRMContentData` 인스턴스를 만듭니다.

   이 코드를 try-catch 블록에 넣습니다.

   ```
   new DRMContentData(metadata_bytes)
   ```

   여기서 `metadata_bytes`은 1단계에서 얻은 `URLLoader` 개체입니다.

   [iOS:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. `DRMManager` 개체에서 전달된 `DRMStatusEvent` 및 `DRMErrorEvent`에 대한 수신기를 만듭니다.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   `DRMStatusEvent` 리스너에서 라이센스가 유효한지(null 아님) 확인합니다. `DRMErrorEvent` 리스너에서 `DRMErrorEvents`을 처리합니다. 이 안내서의 *DRMStatusEvent 클래스 사용* 및 *DRMErrorEvent 클래스 사용*&#x200B;을 참조하십시오.

1. 컨텐츠를 재생하는 데 필요한 라이센스를 로드합니다.
먼저 로컬에 저장된 라이선스를 로드하여 컨텐츠를 재생해 보십시오.

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android:DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   로드가 완료되면 `DRMManager` 개체는 `DRMStatusEvent.DRM_Status`을(를) 전달합니다.

1. `DRMVoucher` 개체를 확인합니다.


   `DRMVoucher` 개체가 null이 아닌 경우 라이선스가 유효합니다. 9단계로 이동합니다.

   [Android:DRMLicenseAcquifiedCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS:DRMLicenseAcquisted](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 이 콘텐트에 대한 정책에 필요한 인증 방법을 확인하십시오.

   `DRMContentData.authenticationMethod` 속성을 사용하십시오.
   1. 인증 방법이 `ANONYMOUS`이면 9단계로 이동합니다. 

      [Android:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 인증 방법이 `USERNAME_AND_PASSWORD`이면 응용 프로그램에서 사용자가 자격 증명을 입력할 수 있는 메커니즘을 제공해야 합니다.

      사용자의 자격 증명을 라이센스 서버에 전달하여 사용자를 인증합니다.

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      인증이 실패할 경우 `DRMManager`, 인증이 성공하면 `DRMAuthenticationErrorEvent`를 전달합니다. `DRMAuthenticationCompleteEvent` 이러한 이벤트에 대한 리스너를 만듭니다.

      [Android:authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS:인증:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe은 자격 증명을 제공하기 위해 더 안전한 메커니즘을 사용하는 것이 좋습니다. 참조하려면 [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html)을 참조하십시오.

   1. 인증 방법이 `UNKNOWN`이면 사용자 지정 인증 방법을 사용해야 합니다.

      이 경우 콘텐츠 제공업체는 Primetime API를 사용하지 않고 대역 외 방식으로 인증을 수행하도록 요청했습니다. 사용자 지정 인증 프로시저는 `DRMManager.setAuthenticationToken()` 메서드에 전달할 수 있는 인증 토큰을 생성해야 합니다.

      [Android:setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS:setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >또는 인증 방법에 관계없이 `.setAuthenticationToken()`을 사용하여 클라이언트에서 라이센스 서버로 사용자 지정 데이터를 보낼 수 있습니다. 이는 API를 과도하게 로드하는 방식입니다. 이 메커니즘은 라이선스 취득 시 클라이언트에서 라이선스 서버로 동적 사용자 지정 데이터를 보내는 유일한 방법입니다. 이 사용자 지정 데이터 전송 방법은 [Primetime DRM(Adobe 액세스) 포럼 ](https://forums.adobe.com/community/adobe_access)의 여러 포럼 게시물에서 자세히 설명합니다.

1. 인증이 실패할 경우 애플리케이션이 6단계로 돌아가야 합니다.

   응용 프로그램에 반복되는 인증 실패를 처리하고 제한하는 메커니즘이 있는지 확인합니다. 예를 들어 세 번 시도한 후 사용자에게 인증이 실패했으며 컨텐츠를 재생할 수 없음을 나타내는 메시지를 표시합니다.
1. 사용자에게 자격 증명을 입력하라는 메시지를 표시하지 않고 저장된 토큰을 사용하려면 토큰을 `DRMManager.setAuthenticationToken()` 메서드로 설정합니다.

   그런 다음 라이센스 서버에서 라이센스를 다운로드하고 6단계에서와 같이 내용을 재생합니다.
   1. **선택 사항:** 인증이 성공하면 메모리에 캐시되는 바이트 배열인 인증 토큰을 캡처할 수 있습니다.

      이 토큰을 `DRMAuthenticationCompleteEvent.token` 속성으로 가져옵니다. 사용자가 이 컨텐츠에 대한 자격 증명을 반복적으로 입력할 필요가 없도록 인증 토큰을 저장하고 사용할 수 있습니다. 라이선스 서버는 인증 토큰의 유효한 기간을 결정합니다.

      [Android:OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS:DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 인증이 완료되면 라이센스 서버에서 라이센스를 다운로드합니다.

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   로드가 완료되면 `DRMManager` 개체는 `DRMStatusEvent.DRM_STATUS`을(를) 전달합니다. 이 이벤트를 수신하고, 전달되면 콘텐트를 재생할 수 있습니다.  Primetime 개체를 만든 다음 해당 `play()` 메서드로 비디오를 재생합니다.

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android:acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)