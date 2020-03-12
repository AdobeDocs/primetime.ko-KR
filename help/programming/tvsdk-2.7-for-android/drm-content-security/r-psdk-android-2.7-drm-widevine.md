---
description: DASH 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.
seo-description: DASH 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.
seo-title: Widevine DRM
title: Widevine DRM
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Widevine DRM {#widevine-drm}

DASH 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.

재생을 시작하기 전에 다음 `com.adobe.mediacore.drm.DRMManager` API를 호출합니다.

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

인수:

* `drm` - `"com.widevine.alpha"` Widevine용.

* `licenseServerURL` - 라이센스 요청을 받은 Widevine 라이센스 서버의 URL.
* `requestProperties` - 나가는 라이선스 요청에 포함할 추가 헤더를 포함합니다.

예를 들어 Expressplay DRM용으로 패키지된 컨텐츠를 사용하는 경우 재생 전에 다음 코드를 사용하십시오.

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

