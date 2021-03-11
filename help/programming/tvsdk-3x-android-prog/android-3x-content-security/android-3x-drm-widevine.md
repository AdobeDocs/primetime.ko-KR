---
description: Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 솔루션 대신 사용할 수 있습니다.
title: 무선 DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# 무선 DRM {#widevine-drm}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 솔루션 대신 사용할 수 있습니다.

제3자 DRM 솔루션 이용에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

HLS CMAF 스트림과 함께 Android 기본 무선 DRM을 사용할 수 있습니다.

>[!NOTE]
>
> Widevine CENC CTR 체계를 사용하려면 최소 Android 버전 4.4(API 레벨 19)가 필요합니다.
>
> 무선 CBCS 체계를 사용하려면 최소 Android 버전 7.1(API 레벨 25)이 필요합니다.

## 라이선스 서버 세부 정보 설정 {#license-server-details}

MediaPlayer 리소스를 로드하기 전에 다음 `com.adobe.mediacore.drm.DRMManager` API를 호출합니다.

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 인수 {#arguments-license-server}

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

## 사용자 지정 콜백 {#custom-callback} 제공

MediaPlayer 리소스를 로드하기 전에 다음 `com.adobe.mediacore.drm.DRMManager` API를 호출합니다.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 인수 {#arguments-custom-callback}

* `callback` - 기본 대신 사용할 MediaDrmCallback의 사용자 지정 구현입니다 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

자세한 내용은 [Android TVSDK 3.11 API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html)를 참조하십시오.

## 현재 로드된 MediaPlayer 리소스 {#pssh-box-mediaplayer-resoource}의 PSSH 상자 가져오기

다음 `com.adobe.mediacore.drm.DRMManager` API를 호출하십시오(가급적이면 사용자 지정 콜백 구현에서).

```java
public static byte[] getPSSH()
```

API는 로드된 무선 미디어 리소스와 관련된 보호 시스템 특정 헤더 상자를 반환합니다.

유효한 상자는 DRM 인스턴스를 만들고 키를 로드하는 동안 짧은 기간 동안 사용할 수 있습니다. `MediaDrmCallback callback executeKeyRequest()` 라이센스 키 가져오기를 사용자 정의하는 데 사용할 수 있습니다.

>[!NOTE]
>
> `getPSSH()` API는 단일 플레이어 인스턴스에서만 지원됩니다. 여러 플레이어나 인스턴트 온 기능을 정확하게 초기화하여 올바른 상자를 받아야 합니다.
