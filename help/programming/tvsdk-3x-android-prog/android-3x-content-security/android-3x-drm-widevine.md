---
description: Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 타사 DRM 솔루션을 Adobe의 통합 솔루션의 대안으로 사용할 수 있습니다.
seo-description: Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 타사 DRM 솔루션을 Adobe의 통합 솔루션의 대안으로 사용할 수 있습니다.
seo-title: Widevine DRM
title: Widevine DRM
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Widevine DRM {#widevine-drm}

Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 타사 DRM 솔루션을 Adobe의 통합 솔루션의 대안으로 사용할 수 있습니다.

타사 DRM 솔루션의 사용 가능성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

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
