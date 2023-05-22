---
description: 클라이언트 코드는 데이터를 Android API에 전달합니다.
title: Android PSDK의 키 요청 워크플로
exl-id: 3ff52c0d-0789-4fe5-bf9d-f03184bad488
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Android PSDK의 키 요청 워크플로{#key-request-workflow-on-android-psdk}

클라이언트 코드는 데이터를 Android API에 전달합니다.

Android에서 클라이언트 코드는 다음 API를 사용하여 라이센스 서버 URL 및 함께 제공되는 라이센스 획득 데이터를 전달해야 합니다.

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

이 API를 성공적으로 호출한 후 코드는 일반적인 방식으로 콘텐츠 재생을 시작할 수 있습니다. Expressplay를 사용하는 경우 토큰을 라이선스 서버 URL의 일부 또는 요청 속성으로 전달하고 라이선스 서버 URL에서 토큰을 제거할 수 있습니다.

일부 Android 장치는 Widevine과 PlayReady를 모두 지원합니다. 이러한 장치에서 고객은 콘텐츠가 여러 개의 DRM 헤더를 가지는 경우 PSDK가 특정 DRM을 사용하여 콘텐츠를 해독하도록 강제할 수 있습니다. 이 작업은 재생 전에 다음 API를 호출하여 수행할 수 있습니다.

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```
