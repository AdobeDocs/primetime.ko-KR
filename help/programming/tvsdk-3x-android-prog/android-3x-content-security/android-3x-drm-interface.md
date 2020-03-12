---
description: Primetime DRM 솔루션의 주요 클라이언트측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 특정 DRM 작업을 보다 쉽게 구현할 수 있도록 하는 데 사용할 수 있는 DRMHelper 클래스도 포함되어 있습니다.
seo-description: Primetime DRM 솔루션의 주요 클라이언트측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 특정 DRM 작업을 보다 쉽게 구현할 수 있도록 하는 데 사용할 수 있는 DRMHelper 클래스도 포함되어 있습니다.
seo-title: Primetime DRM 인터페이스 개요
title: Primetime DRM 인터페이스 개요
uuid: 9e6f6ae6-7193-40fe-bc9d-d8de33705f5d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Primetime DRM 인터페이스 개요 {#primetime-drm-interface-overview}

Primetime DRM 솔루션의 주요 클라이언트측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 응용 프로그램에는 특정 DRM 작업을 구현하기 쉽게 하는 데 사용할 수 있는 `DRMHelper` 클래스가 포함되어 있습니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM은 TVSDK 애플리케이션에서 컨텐츠 보호를 구현하는 확장 가능하고 효율적인 워크플로우를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 만들어 비디오 컨텐츠에 대한 권한을 보호하고 관리할 수 있습니다.

자세한 내용은 TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM 작업을 위한 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어의 참조입니다.

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >이 API 파섹 `DRMManager` `MediaPlayerEvent.DRM_METADATA` 이 이벤트가 `getDRMManager()` 실행되기 전에 호출하면 NULL이 반환될 수 있습니다.

* DRM 워크플로우를 구현할 때 유용한 `DRMHelper` 도우미 클래스입니다.
* DRM 메타데이터가 미디어의 개별 URL에 있을 때 로드되는 `DRMHelper` 메타데이터 로더 메서드입니다.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* DRM 메타데이터를 확인하고 인증이 필요한지 여부를 확인하는 `DRMHelper` 방법입니다.

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

* `DRMHelper` 메서드를 사용하여 인증 수행

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

* 응용 프로그램에 다양한 DRM 활동 및 상태를 알려주는 이벤트입니다.

DRM에 대한 자세한 내용은 DRM [설명서를](https://helpx.adobe.com/primetime/user-guide.html)참조하십시오.
