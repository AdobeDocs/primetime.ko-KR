---
description: Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 타사 DRM 솔루션을 Adobe의 통합 솔루션 대신 사용할 수 있습니다.
title: 와이드빈
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 와이드빈 {#widevine-drm}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 타사 DRM 솔루션을 Adobe의 통합 솔루션 대신 사용할 수 있습니다.

타사 DRM 솔루션의 가용성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

HLS CMAF 스트림과 함께 Android 기본 Widevine DRM을 사용할 수 있습니다.

>[!NOTE]
>
> Widevine CENC CTR 구성표에는 최소 Android 버전 4.4(API 레벨 19)가 필요합니다.
>
> Widevine CBCS 구성표에는 최소 Android 버전 7.1(API 레벨 25)이 필요합니다.

## 라이선스 서버 세부 정보 설정 {#license-server-details}

다음을 호출합니다 `com.adobe.mediacore.drm.DRMManager` MediaPlayer 리소스를 로드하기 전 API:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 인수 {#arguments-license-server}

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

## 사용자 지정 콜백 제공 {#custom-callback}

다음을 호출합니다 `com.adobe.mediacore.drm.DRMManager` MediaPlayer 리소스를 로드하기 전 API입니다.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 인수 {#arguments-custom-callback}

* `callback` - 기본값 대신 사용할 MediaDrmCallback의 사용자 지정 구현 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

자세한 내용은 [Android TVSDK 3.11 API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## 현재 로드된 MediaPlayer 리소스의 PSSH 상자 가져오기 {#pssh-box-mediaplayer-resoource}

다음을 호출합니다 `com.adobe.mediacore.drm.DRMManager` API, 바람직하게는 사용자 지정 콜백 구현입니다.

```java
public static byte[] getPSSH()
```

API는 로드된 Widevine 미디어 리소스와 연결된 보호 시스템별 헤더 상자를 반환합니다.

짧은 기간(DRM 인스턴스 생성과 키 로드 사이)에 유효한 상자를 사용할 수 있습니다. `MediaDrmCallback callback executeKeyRequest()` 라이선스 키 가져오기를 사용자 지정하는 데 사용할 수 있습니다.

>[!NOTE]
>
> `getPSSH()` API는 단일 플레이어 인스턴스에서만 지원됩니다. 여러 플레이어 또는 Instant On 기능을 연속으로 초기화해야 올바른 상자를 받을 수 있습니다.
