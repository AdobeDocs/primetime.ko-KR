---
description: 클라이언트 코드는 데이터를 Android API로 전달합니다.
seo-description: 클라이언트 코드는 데이터를 Android API로 전달합니다.
seo-title: Android PSDK의 주요 요청 워크플로우
title: Android PSDK의 주요 요청 워크플로우
uuid: 575163de-0f96-434d-a3ff-7e114caf72de
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Android PSDK{#key-request-workflow-on-android-psdk}의 키 요청 워크플로우

클라이언트 코드는 데이터를 Android API로 전달합니다.

Android의 경우 클라이언트 코드가 다음 API를 사용하여 라이센스 서버 URL 및 포함된 라이센스 획득 데이터를 전달해야 합니다.

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

이 API를 성공적으로 호출하면 코드가 일반적인 방식으로 컨텐츠 재생을 시작할 수 있습니다. Express를 사용하는 경우 토큰을 라이센스 서버 URL의 일부나 요청 속성으로 전달하고 라이선스 서버 URL에서 토큰을 제거할 수 있습니다.

일부 Android 장치는 Widevine 및 PlayReady를 모두 지원합니다. 이러한 장치에서 고객은 컨텐트에 여러 DRM 헤더가 있는 경우 특정 DRM을 사용하여 컨텐츠의 암호를 해독해야 할 수 있습니다. 재생 전에 다음 API를 호출하여 수행할 수 있습니다.

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

