---
description: Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 Adobe의 통합 Primetime DRM 솔루션 대신 타사 DRM 솔루션을 사용할 수 있습니다.
title: Primetime DRM 인터페이스 개요
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 개요 {#primetime-drm-interface-overview}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 Adobe의 통합 Primetime DRM 솔루션 대신 타사 DRM 솔루션을 사용할 수 있습니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

타사 DRM 솔루션의 가용성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

Primetime DRM(디지털 권한 관리) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 `DRMHelper` 특정 DRM 작업을 보다 쉽게 구현하는 방법을 보여 주는 클래스입니다.

Primetime DRM은 TVSDK 애플리케이션에서 콘텐츠 보호를 구현할 수 있는 확장 가능한 효율적인 워크플로를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 만들어 비디오 콘텐츠에 대한 권한을 보호하고 관리합니다.

TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM 작업을 위한 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어의 참조:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >이 API는 유효한 을(를) 반환합니다 `DRMManager` 개체 `MediaPlayerEvent.DRM_METADATA` 이(가) 실행되었습니다. 전화 주시면 `getDRMManager()` 이 이벤트가 실행되기 전에 NULL을 반환할 수 있습니다.

* 다음 `DRMHelper` helper 클래스 : DRM 워크플로우를 구현할 때 유용합니다.

  다음을 볼 수 있습니다. `DRMHelper` 위치: `ReferencePlayer`.

* A `DRMHelper` DRM 메타데이터가 미디어와 별도의 URL에 있는 경우 로드하는 메타데이터 로더 방법.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` 인증이 필요한지 여부를 확인하기 위해 DRM 메타데이터를 확인하는 방법입니다.

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

* `DRMHelper` 인증을 수행하는 방법입니다.

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

* 다양한 DRM 활동 및 상태에 대해 애플리케이션에 알리는 이벤트입니다.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

추가적인 관련 API 요소:

* [com.adobe.ave.drm.DRMMmanager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
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

DRM에 대한 자세한 내용은 [Adobe Primetime DRM 설명서](https://helpx.adobe.com/primetime/user-guide.html).
