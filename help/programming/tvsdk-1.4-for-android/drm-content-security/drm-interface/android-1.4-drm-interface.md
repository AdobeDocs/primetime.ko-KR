---
description: Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 Primetime DRM 솔루션의 대안으로 사용할 수 있습니다.
title: Primetime DRM 인터페이스 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# 개요 {#primetime-drm-interface-overview}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 Primetime DRM 솔루션의 대안으로 사용할 수 있습니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

제3자 DRM 솔루션의 사용 가능성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

Primetime 디지털 저작권 관리(DRM) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 응용 프로그램에는 특정 DRM 작업을 구현하기 쉽게 하는 방법을 보여 주는 `DRMHelper` 클래스가 포함되어 있습니다.

Primetime DRM은 TVSDK 애플리케이션에서 컨텐츠 보호를 구현하는 확장 가능하고 효율적인 워크플로우를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 생성하여 비디오 컨텐츠에 대한 권한을 보호하고 관리할 수 있습니다.

TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM에서 작업하는 데 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어 참조:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >이 API는 `MediaPlayerEvent.DRM_METADATA`이(가) 실행된 후에만 유효한 `DRMManager` 개체를 반환합니다. 이 이벤트가 발생하기 전에 `getDRMManager()`을(를) 호출하면 NULL이 반환될 수 있습니다.

* DRM 작업 과정을 구현할 때 유용한 `DRMHelper` 도우미 클래스입니다.

   `ReferencePlayer`에 `DRMHelper`이 표시됩니다.

* 미디어와 별도의 URL에 있을 때 DRM 메타데이터를 로드하는 `DRMHelper` 메타데이터 로더 메서드입니다.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* 인증이 필요한지 여부를 확인하기 위해 DRM 메타데이터를 확인하는 `DRMHelper` 메서드입니다.

   ```java
   /** 
   * Return whether authentication is needed for the provided 
   * DRMMetadata. 
   * 
   * @param drmMetadata 
   * The desired DRMMetadata on which to check whether auth is needed. 
   * @return whether authentication is required for the provided metadata 
   */ 
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

* `DRMHelper` 인증 수행 방법

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
   * @param authUser 
   * the DRM username provider by the user. 
   * @param authPass 
   * the DRM password provided by the user. 
   */ 
   public static void performDrmAuthentication(final DRMManager drmManager,  
   final DRMMetadata drmMetadata,  
   final String authUser,  
   final String authPass,  
   final DRMAuthenticationListener authenticationListener);
   ```

* 응용 프로그램에 다양한 DRM 활동 및 상태를 알리는 이벤트입니다.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

추가 관련 API 요소:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

DRM에 대한 자세한 내용은 [Adobe Primetime DRM 설명서](https://helpx.adobe.com/primetime/user-guide.html)를 참조하십시오.
