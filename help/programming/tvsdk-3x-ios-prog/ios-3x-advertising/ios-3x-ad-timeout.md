---
description: Adobe Primetime 광고 결정 인터페이스를 사용하여 VOD 및 라이브/선형 콘텐츠에 광고를 삽입할 수 있습니다.
title: 광고 요구 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 광고 시간 초과 {#ad-timeout}

## AV Foundation 요구 사항 {#av-foundation-requirements}

VOD 콘텐츠의 경우, 기본 콘텐츠 매니페스트 로드, 광고 해상도 및 광고 매니페스트 로드가 포함된 재생 목록 결합은 35초 이내에 완료되어야 합니다.

라이브 콘텐츠의 경우 재생 목록이 업데이트될 때마다 재생 목록 결합은 20초 이내에 완료되어야 합니다

**AdResolution 시간 초과와 관련된 API**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

광고 메타데이터를 설정할 때 PTAdMetadata::adResolutionTimeout을 설정하여 adResolutionTimeout을 설정할 수 있습니다.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

그런 다음 다음 섹션을 수행합니다. [Primetime 광고 서버 메타데이터](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**AdManifest 시간 초과와 관련된 API**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

광고 메타데이터를 설정할 때 PTAdMetadata::adManifestTimeout을 설정하여 adManifestTimeout을 설정할 수 있습니다.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

그런 다음 다음 섹션을 수행합니다. [Primetime 광고 서버 메타데이터](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
