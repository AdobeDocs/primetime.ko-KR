---
description: Primetime 플레이어는 Primetime DRM 통합을 사용자 지정 DRM 워크플로우로 지원합니다. 즉, 애플리케이션이 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다.
title: DRM 콘텐츠 보호
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# DRM 콘텐츠 보호 {#drm-content-protection}

Primetime 플레이어는 Primetime DRM 통합을 사용자 지정 DRM 워크플로우로 지원합니다. 즉, 애플리케이션이 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다.

이를 활성화하기 위해 TVSDK는 인증을 위한 DRM 관리자를 제공합니다. 참조 구현은 다음 워크플로의 예를 제공합니다.

* 낮은 오류율과 빠른 시작에 최적화된 액세스 콘텐츠 보호를 사용하여 HLS 스트림을 로드하고 재생하는 방법
* AES128 콘텐츠 보호를 사용하여 HLS 스트림을 로드하고 재생하는 방법.
* 낮은 오류율과 빠른 시작에 최적화된 PHLS 콘텐츠 보호를 사용하여 HLS 스트림을 로드하고 재생하는 방법입니다.

모든 DRM 보호 콘텐츠는 TVSDK에 내장된 DRM 라이브러리에 의해 자동으로 처리됩니다. 그러나 TVSDK API 콜백을 사용하여 오류 처리, 장치 개별화 최적화 및 라이선스 획득을 노출할 수 있습니다.

## 플레이어에 콘텐츠 보호 추가 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

재생 관리자를 만들거나 관리자 팩토리를 사용하여 플레이어에 콘텐츠 보호를 추가할 수 있습니다.

콘텐츠 보호 관리자를 만들려면 다음 작업을 수행하십시오.

* DRM 시스템을 초기화합니다.

  다음 코드 예제에서는 호출을 보여 줍니다 `loadDRMServices` 응용 프로그램에서 `onCreate()` 함수를 사용하여 DRM 시스템에 필요한 초기화가 재생 시작 전에 시작되도록 할 수 있습니다.

  ```java
  @Override 
   public void onCreate() { 
       super.onCreate();  
       DrmManager.loadDRMServices(getApplicationContext()); 
   }
  ```

* DRM 라이센스를 미리 로드합니다.

  다음 코드 예제에서는 `VideoItems` 콘텐츠 목록 로드가 완료되면. 이렇게 하면 DRM 라이선스가 라이선스 서버에서 획득되고 로컬로 캐시되므로 재생이 시작될 때 콘텐츠가 최소 지연으로 로드됩니다.

  ```java
  DrmManager.preLoadDrmLicenses(item.getUrl(),  
    new MediaPlayerItemLoader.LoaderListener() { 
  
      @Override 
      public void onLoadComplete(MediaPlayerItem item) { 
          Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
      } 
  
      @Override 
      public void onError(MediaErrorCode errorCode, String s) { 
          Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
      } 
  } 
  ```

  >[!NOTE]
  >
  >설정 사용자 인터페이스에서 사전 캐싱 DRM 라이센스 를 설정(ON)으로 설정하여 콘텐츠를 로드할 때 DRM 라이센스를 사전 캐싱할 수 있습니다. 그러나 카탈로그의 모든 라이센스에 미리 로드하는 대신 특정 항목을 미리 로드하는 것이 가장 좋습니다.
  >
  >![](assets/precache-drm-licenses.jpg)

* 사용 `ManagerFactory` DRM 오류 처리를 구현하려면 다음 코드 줄이 [!DNL PlayerFragment.java] 파일:

  ```java
  drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
  ```

**관련 API 설명서**

* [클래스 DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListen](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
