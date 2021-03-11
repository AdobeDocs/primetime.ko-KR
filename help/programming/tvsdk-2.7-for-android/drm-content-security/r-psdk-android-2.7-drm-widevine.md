---
description: DASH 스트림과 함께 Android 기본 무선 DRM을 사용할 수 있습니다.
title: 무선 DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# 무선 DRM {#widevine-drm}

DASH 스트림과 함께 Android 기본 무선 DRM을 사용할 수 있습니다.

재생을 시작하기 전에 다음 `com.adobe.mediacore.drm.DRMManager` API를 호출합니다.

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

인수:

* `drm` -  `"com.widevine.alpha"` Widevin용

* `licenseServerURL` - 라이센스 요청을 받은 무선 라이센스 서버의 URL.
* `requestProperties` - 나가는 라이선스 요청에 포함할 추가 헤더를 포함합니다.

예를 들어 Expressplay DRM용으로 패키지된 내용을 사용할 때 재생 전에 다음 코드를 사용하십시오.

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

