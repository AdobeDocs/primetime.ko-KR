---
description: Primetime 플레이어는 사용자 정의 DRM 워크플로우로서 Primetime DRM 통합을 지원합니다. 즉, 응용 프로그램이 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다.
seo-description: Primetime 플레이어는 사용자 정의 DRM 워크플로우로서 Primetime DRM 통합을 지원합니다. 즉, 응용 프로그램이 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다.
seo-title: DRM 컨텐츠 보호
title: DRM 컨텐츠 보호
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# DRM 컨텐츠 보호 {#drm-content-protection}

Primetime 플레이어는 사용자 정의 DRM 워크플로우로서 Primetime DRM 통합을 지원합니다. 즉, 응용 프로그램이 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다.

이를 활성화하기 위해 TVSDK는 인증을 위한 DRM 관리자를 제공합니다. 참조 구현에서는 다음 워크플로우의 예를 제공합니다.

* 낮은 오류 속도와 빠른 시작을 위해 최적화된 액세스 컨텐츠 보호를 사용하여 HLS 스트림을 로드하고 재생하는 방법.
* AES128 컨텐츠 보호를 사용하여 HLS 스트림을 로드하고 재생하는 방법
* 낮은 오류 속도와 빠른 시작을 위해 최적화된 PHLS 컨텐츠 보호 기능을 사용하여 HLS 스트림을 로드하고 재생하는 방법

TVSDK에 내장된 DRM 라이브러리를 통해 모든 DRM으로 보호된 콘텐츠를 자동으로 처리할 수 있습니다. 그러나 TVSDK API 콜백을 사용하여 오류 처리, 장치 개인화의 최적화 및 라이센스 획득을 노출할 수 있습니다.

## 플레이어 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}에 컨텐츠 보호 추가

재생 관리자를 만들거나 관리자 팩터리를 사용하여 플레이어에 컨텐츠 보호를 추가할 수 있습니다.

컨텐츠 보호 관리자를 만들려면

* DRM 시스템을 초기화합니다.

   다음 코드 예제는 재생 시작 전에 DRM 시스템에 필요한 초기화가 시작되도록 응용 프로그램 `onCreate()` 함수에서 `loadDRMServices`을 호출하는 방법을 보여줍니다.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* DRM 라이선스 미리 로드

   다음 코드 예제는 콘텐트 목록 로드가 완료된 경우 `VideoItems`을 로드하는 것을 보여줍니다. 이로 인해 라이센스 서버에서 DRM 라이센스를 획득하여 로컬에 캐시하여 재생을 시작할 때 컨텐츠가 최소 지연 없이 로드됩니다.

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
   >콘텐츠를 로드할 때 DRM 라이선스를 미리 캐시하도록 설정 사용자 인터페이스에서 Precache DRM 라이선스를 ON으로 설정할 수 있습니다. 하지만 카탈로그의 모든 라이선스를 미리 받는 대신 특정 항목을 미리 로드하는 것이 좋습니다.
   >
   >![](assets/precache-drm-licenses.jpg)

* `ManagerFactory`을(를) 사용하여 DRM 오류 처리를 구현하려면 다음 코드 줄이 [!DNL PlayerFragment.java] 파일에 있는지 확인하십시오.

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**관련 API 설명서**

* [클래스 DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)