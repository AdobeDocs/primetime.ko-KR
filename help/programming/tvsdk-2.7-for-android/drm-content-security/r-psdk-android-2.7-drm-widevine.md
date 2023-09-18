---
description: DASH 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.
title: 와이드빈
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 와이드빈 {#widevine-drm}

DASH 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.

다음을 호출합니다 `com.adobe.mediacore.drm.DRMManager` 재생을 시작하기 전 API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

인수:

* `drm` - `"com.widevine.alpha"` Widevine을 위해.

* `licenseServerURL` - 라이센스 요청을 받는 Widevine 라이센스 서버의 URL.
* `requestProperties` - 보내는 라이선스 요청에 포함할 추가 헤더를 포함합니다.

예를 들어 Expressplay DRM용으로 패키지된 콘텐츠를 사용하는 경우 재생하기 전에 다음 코드를 사용하십시오.

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
