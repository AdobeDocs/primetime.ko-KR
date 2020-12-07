---
description: Primetime DRM 솔루션의 주요 클라이언트 측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 DRM 작업을 보다 쉽게 구현할 수 있도록 사용할 수 있는 DRMHelper 클래스도 포함되어 있습니다.
seo-description: Primetime DRM 솔루션의 주요 클라이언트 측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 DRM 작업을 보다 쉽게 구현할 수 있도록 사용할 수 있는 DRMHelper 클래스도 포함되어 있습니다.
seo-title: Primetime DRM 인터페이스 개요
title: Primetime DRM 인터페이스 개요
uuid: d77a98c8-c1f5-4fe3-8d0b-3d21e288f228
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Primetime DRM 인터페이스 개요 {#primetime-drm-interface-overview}

Primetime DRM 솔루션의 주요 클라이언트 측 요소는 DRM 관리자입니다. Android SDK에 포함된 샘플 애플리케이션에는 DRM 작업을 보다 쉽게 구현할 수 있도록 사용할 수 있는 DRMHelper 클래스도 포함되어 있습니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM은 TVSDK 애플리케이션에서 컨텐츠 보호를 구현하는 확장 가능하고 효율적인 워크플로우를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 생성하여 비디오 컨텐츠에 대한 권한을 보호하고 관리할 수 있습니다.

자세한 내용은 TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM 작업을 위한 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어 참조:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >이 API는 `MediaPlayerEvent.DRM_METADATA`이(가) 실행된 후에만 유효한 `DRMManager` 개체를 반환합니다. 이 이벤트가 실행되기 전에 `getDRMManager()`을 호출하면 NULL이 반환될 수 있습니다.

* DRM 작업 과정을 구현할 때 유용한 `DRMHelper` 도우미 클래스입니다.
* 미디어와 별도의 URL에 있는 경우 DRM 메타데이터를 로드하는 `DRMHelper` 메타데이터 로더 메서드입니다.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* DRM 메타데이터를 확인하고 인증이 필요한지 여부를 확인하는 `DRMHelper` 메서드입니다.

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

* 응용 프로그램에 다양한 DRM 활동 및 상태를 알려주는 이벤트입니다.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

DRM에 대한 자세한 내용은 [DRM 설명서](https://helpx.adobe.com/primetime/user-guide.html)를 참조하십시오.
