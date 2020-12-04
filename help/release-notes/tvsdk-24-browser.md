---
title: 브라우저 TVSDK 2.4 릴리스 노트
seo-title: 브라우저 TVSDK 2.4 릴리스 노트
description: 브라우저 TVSDK 2.4 릴리스 노트는 Browser TVSDK 2.4의 새로운 기능, 지원 및 지원되지 않는 기능 및 알려진 문제에 대해 설명합니다.
seo-description: 브라우저 TVSDK 2.4 릴리스 노트는 Browser TVSDK 2.4의 새로운 기능, 지원 및 지원되지 않는 기능 및 알려진 문제에 대해 설명합니다.
uuid: 3a1eb1a5-0e72-4658-beeb-bca8816570e7
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: d71886cb-f34b-47b2-9df7-168686478106
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '6834'
ht-degree: 0%

---


# 브라우저 TVSDK 2.4 릴리스 노트 {#browser-tvsdk-release-notes}

브라우저 TVSDK 2.4 릴리스 노트는 Browser TVSDK 2.4의 새로운 기능, 지원 및 지원되지 않는 기능 및 알려진 문제에 대해 설명합니다.

## 소개 {#introduction}

Browser TVSDK는 브라우저 기반의 비디오 플레이어 애플리케이션에 고급 비디오 재생 기능, 컨텐츠 보호 및 광고를 추가할 수 있는 툴킷입니다.

Browser TVSDK 2.4는 브라우저 기반 비디오 애플리케이션을 구축할 수 있는 JavaScript API를 제공하며 다음 모드에서 재생 지원을 포함합니다.

* HTML5만 해당
* 자동 플래시 폴백을 사용하는 HTML5
* Flash은 항상

이 릴리스에는 다음 정보가 포함됩니다.

・ [브라우저 TVSDK API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [브라우저 TVSDK 프로그래밍 가이드](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [TVSDK for 1.4 DHLS에서 Browser TVSDK 2.4 Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)

・ [Browser TVSDK 2.4.6에서 버전 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html)으로 변환

・ 빌드에 포함된 참조 구현

>[!NOTE]
>
>*이 릴리스에 대한 보안 고려 사항 전체 목록은 보안 고려 사항을 참조하십시오.

## 새로운 기능 및 지원되는 기능 {#what-s-new-and-supported-features}

이 Browser TVSDK 릴리스는 비디오 애플리케이션을 향상시키는 데 사용할 수 있는 새로운 기능을 제공합니다.

**2.4.12 업데이트(빌드 204)의 새로운 기능**

Browser TVSDK 2.4.12 Update(Build 204)의 일부로 다음 추가 기능을 사용할 수 있습니다.

* 재생이 음소거 상태일 때 iOS에서 자동 재생을 허용하도록 AdobePSDK.MediaPlayer의 볼륨 API 구현이 변경되었습니다.

・ Auditude 서버로부터 받은 VPAID 광고를 무시하도록 새로운 API `auditudeSettings.ignoreVPAIDAds`가 추가되었습니다. Flash 폴백에서는 API가 작동하지 않습니다.

**버전 2.4.11**

다음 개선 사항 및 추가 사항은 Browser TVSDK 2.4.11 릴리스의 일부로 사용할 수 있습니다.

・ HLS 라이브 세그먼트 페일오버는 MSE 및 Flash 폴백 모드에서 지원됩니다.

・ MSE에서도 `AuditudeSettings.creativeRepackagingDomain` API에 대한 지원을 사용할 수 있습니다. 이전에는 Flash 폴백 모드에서만 지원되었습니다.

・ 이번 릴리스에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. *문제가 해결되었습니다.* 목록을 참조하십시오.

**버전 2.4.10**

Browser TVSDK 2.4.10 릴리스의 일부로 다음과 같은 향상된 기능과 추가 기능을 사용할 수 있습니다.

・ TVSDK는 로깅을 활성화하거나 비활성화할 수 있는 enableLogging()을 제공합니다. 사용법은 [API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)를 참조하십시오.

・ TVSDK는 Adobe Analytics 사용 시 기본 장을 더 이상 지원하지 않습니다. 애플리케이션을 사용하여 장을 정의하고 관리할 수 있습니다.

・ 이번 릴리스에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. *해결된 문제 *목록을 참조하십시오.

**버전 2.4.9**

Browser TVSDK 2.4.9 릴리스의 일부로 다음과 같은 향상된 기능과 추가 기능을 사용할 수 있습니다.

・ 시간 불연속성이 있는 HLS VOD 및 라이브 스트림이 지원되지만 무중단 운영 마커는 지원되지 않습니다.

・ ID3 v2.4.0 프레임은 HLS VOD 및 실시간 스트림을 위한 Safari 비디오 태그에서 지원됩니다.

・ 안전한 광고 로드 구현을 통해 광고 서버 호출이 API 구성에 따라 안전한 HTTP로 업그레이드됩니다. 자세한 내용은 AdobePSDK.AdvertisingMetadata 및 AdobePSDK.ForceHttpsAdConfiguration 클래스를 참조하십시오. 이 기능은 Flash 폴백 모드에서 지원되지 않습니다.

・ VAST 3.0 응답과 관련된 광고 ID 정보 및 익스텐션 정보는 이제 TVSDK에서 응용 프로그램에 사용할 수 있으며 광고 측정을 위한 해자 통합을 구현하는 데 사용할 수 있습니다. 자세한 내용은 AdobePSDK.NetworkAdInfo API를 참조하십시오. Flash 폴백 모드에서는 지원되지 않습니다.

・ AdobePSDK.ForceHttpsConfiguration 클래스는 더 이상 사용할 수 없습니다. 성공

AdobePSDK.ForceHttpsAdConfiguration 클래스입니다.

・ 이제 새로운 API인 AdobePSDK.optimizeFlashCalls를 사용하여 Flash 폴백 모드에서 HLS 재생 환경을 개선하기 위한 호출을 최적화할 수 있습니다. 기본적으로 비활성화되어 있습니다.

**2.4.8 업데이트의 새로운 기능 (빌드 6002)**

이 업데이트에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 목록에 대해서는 *고정 문제*&#x200B;를 참조하십시오.

**버전 2.4.9**

Browser TVSDK 2.4.8 릴리스의 일부로 다음과 같은 향상된 기능과 추가 기능을 사용할 수 있습니다.

・ SDK가 이제 Chrome EME와 호환되고 Chrome v58부터 사용 가능한 모범 사례 변경 사항이 적용됩니다. 자세한 내용은 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**를 참조하십시오.

・ 이제 UI 프레임워크는 Flash, 광고 전용 및 타깃팅 정보 워크플로우에서 HLS 액세스 DRM을 지원합니다.

・ setDRMAuthenticateData API가 UI 프레임워크에 추가됩니다. Adobe 액세스 DRM으로 보호된 스트림을 재생하려면 이 API를 불러옵니다. 또는, drmAuthenticateData 속성을 플레이어에서 지정할 수 있습니다. 자세한 내용은 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)을 참조하십시오.

**버전 2.4.7**

버전 2.4.7의 새로운 기능은 다음과 같습니다.

・ UI 프레임워크에서 UI Configurator 추가

다음 방법 중 하나로 플레이어를 구성할 수 있습니다.

・ JSON 개체 사용

・ API 사용

JSON 개체를 생성하는 데 도움이 되는 브라우저 TVSDK는 **UI 구성자 **도구를 제공합니다.

이 도구에서 다양한 설정을 선택하고 **테스트 구성 **을 클릭하여 설정을 확인하고 **구성 다운로드 **를 클릭하여 설정을 다운로드할 수 있습니다. 파일을 다운로드한 후 이 파일의 내용을 JSON 개체로 ptp.videoPlayer API에 전달할 수 있습니다.

・ UI 프레임워크에 MediaPlayerItemConfig API 추가

advertisingMetadata, advertisingFactory, adSigningMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration 등 다양한 기능을 MediaPlayerItem을 통해 구성할 수 있습니다. 자세한 내용은 [브라우저 TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)의 AdobePSDK.MediaPlayerItemConfig 설명서를 참조하십시오.

UI 프레임워크에서 플레이어 구성을 통해 네트워크 구성을 전달하는 방법이 수정되었습니다.

**버전 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**버전 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* UI 프레임워크에서 DRM 및 분석 워크플로우 지원

UI 프레임워크를 통해 DRM 구성 및 분석 추적을 활성화할 수 있습니다.

* `AdobePSDK.embedSWFinFullScreenDiv` API 추가

이 새로운 API는 Flash폴백.swf 파일을 포함할 수 있는 div를 선택할 수 있는 플레이어 앱에 유연성을 제공합니다.

* TVSDK 버전 관련 정보에 대해 `AdobePSDK.MediaPlayer` 클래스의 `getVersion`API를 `AdobePSDK.Version` 클래스로 대체했습니다. 자세한 내용은 `AdobePSDK.Version` API [여기](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html)를 참조하십시오.

**버전 2.4.6**

버전 2.4.6의 새로운 기능은 다음과 같습니다.

* **검색 지원**

브라우저 일련화를 사용하면 브라우저에서 node.js 스타일 모듈을 사용할 수 있습니다. 종속성을 정의하고 찾아보기를 통해 모든 항목을 하나의 JavaScript 파일에 번들로 통합할 수 있습니다.

* **청구**

요금 청구를 통해 Browser TVSDK는 Primetime 고객에게 비용을 청구하기 위해 플레이어 사용량 측정 지표를 수집할 수 있습니다.

>[!NOTE]
>
>더 이상 사용되지 않는 enum MediaPlayer.Events 및 Enum PSDKErrorCode의 더 이상 사용되지 않는 상수가 버전 2.4.6에서 제거되었습니다. 자세한 내용은 [Browser SDK 2.4.5에서 버전 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html)으로 변환을 참조하십시오.

**버전 2.4.5**

버전 2.4.5의 새로운 기능은 다음과 같습니다.

* **전체 이벤트 재생 및 광고**

   이제 HLS FER(Full Event Replay) 스트림이 광고 해상도 및 광고 비헤이비어를 지원합니다. 이 지원을 활성화하려면 `MediaPlayerItemConfig` 개체를 만들 때 광고 신호 모드를 `MANIFEST_CUES`으로 설정합니다.

* **MediaplayerView ScalePolicy 지원**

   애플리케이션 개발자는 이제 MediaplayerView scalePolicy 속성을 사용하여 뷰에 대해 다른 scalePolicy를 지정할 수 있습니다.

* **아나모픽 컨텐츠 지원**

   이제 MSE 및 Flash 재생을 사용할 때 아나모픽 컨텐츠 재생이 지원됩니다.

* **Selective application of`withCredentials`**

`withCredentials`이 true로 설정된 경우 `Access-Control-Allow-Origin` 헤더를 와일드 카드로 설정할 수 없습니다. 서버 응답에 따라 브라우저 TVSDK는 선택적으로 `withCredentials` 속성을 설정합니다. 이 지원에 대한 자세한 내용은 [브라우저 TVSDK API 문서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)를 참조하십시오.

**버전 2.4.4**

버전 2.4.4의 새로운 기능은 다음과 같습니다.

* **Chromecast 샘플 앱**

이 릴리스는 클라이언트측 광고 삽입으로 DASH VOD 스트림 및 DASH Widevine 스트림을 재생하는 방법을 보여 주는 발신자 및 수신자 앱에 대한 지원을 제공합니다.

* **고급 페일오버 지원**

이 릴리스에는 HLS VOD 스트림에 대한 고급 장애 조치(segment and server failover) 사용 사례 지원이 포함되어 있습니다.

**버전 2.4.3**

버전 2.4.3의 새로운 기능은 다음과 같습니다.

* **DASH VOD용 사용자 정의 태그**

   인라인 사용자 지정 태그(이벤트)는 TimedMetadata 개체로 가입하고 수신할 수 있습니다.

* **익스텐션이 없는 스트림 재생**

   이제 확장 기능이 없는 HLS 및 DASH 스트림이 지원됩니다. 매니페스트 파일의 경우 리소스를 로드할 때 resourceType을 지정해야 합니다. 세그먼트 및 VTT 파일의 경우 컨텐츠 유형을 결정하는 데 컨텐츠 유형 응답 헤더를 사용합니다.

**버전 2.4.2**

버전 2.4.2의 새로운 기능은 다음과 같습니다.

* **API 패리티**

API 패리티의 전체 목록은 [TVSDK for 1.4 DHLS에서 브라우저 TVSDK 2.4 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)를 참조하십시오.

* **샘플 AES 지원**

   이 릴리스에서는 MSE 및 Flash 폴백에서 Sample-AES 암호화된 컨텐츠 재생을 지원합니다. Google Chrome에서 보안 원본 위에 AES 컨텐츠를 호스팅해야 하는 요구 사항이 제거되었습니다.

* **AAC 컨테이너 지원**

   이제 .aac 확장자가 있는 파일의 재생이 지원됩니다. 오디오 전용 스트림 또는 대체 오디오가 될 수 있습니다.

   >[!NOTE]
   >
   >AC3 및 향상된 AC3 코덱은 아직 지원되지 않습니다.

* **토큰화된 스트림 재생**

CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 종종 매니페스트에 인증 토큰을 사용하고 검증을 위해 세그먼트 요청을 사용할 수 있으며 이러한 토큰을 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다. 이제 이러한 스트림의 재생이 지원됩니다.

**버전 2.4.1**

버전 2.4.1의 새로운 기능은 다음과 같습니다.

* **UI 프레임워크**

JavaScript 기반 비디오 플레이어 응용 프로그램의 UI 개발을 가속화하기 위해 고안된 이 프레임워크는 재생/일시 정지 및 볼륨 등의 기본 컨트롤을 포함하는 API와 스크러빙 막대 상태 및 닫힌 캡션 설정과 같은 요소를 쉽게 추가 또는 제거하기 위해 고안되었습니다. 컨트롤과 관련된 동작을 지정하고, 사용자 정의 컨트롤을 만들고, 플레이어 UI에 스킨을 지정할 수 있습니다. 이러한 모든 작업은 프레임워크를 통해 이루어지며 DOM 구조를 직접 조작할 필요가 없습니다.

* **라이브 스트림의 향상된 HLS 재생**

이 릴리스는 광고 삽입으로 인한 불연속성을 지원합니다. EXT-PROGRAM-DATE-TIME 태그 뒤에 EXT-MEDIA-SEQUENCE 태그를 사용하여 매끄러운 재생을 위해 적응형 비트 전송률 프로필 간에 동기화합니다.

* **VPAID 2.0 지원**

비디오 플레이어 광고 서비스 인터페이스 정의(VPAID) 버전 2.0은 사용자를 위해 풍부한 미디어 경험을 제공하고 발행자는 광고를 더 잘 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있도록 합니다. 이 릴리스는 VOD(Video-On-Demand) 컨텐츠를 위한 선형 JavaScript VPAID 광고를 지원합니다.

* **사용자 지정 HLS 태그**

미디어 스트림에는 재생 목록/매니페스트 파일의 태그 형태로 추가 메타데이터가 포함될 수 있습니다. Browser TVSDK를 사용하면 추가 태그를 지정하고 가입할 수 있으며 해당 태그가 매니페스트에 표시될 때 알림을 받을 수 있습니다.

* **플레이어 타임라인에 표시되는 광고 마커**

이 릴리스는 VOD 및 라이브 컨텐츠 모두에 대해 플레이어 타임라인에 광고 마커 표시를 지원합니다. 참조 플레이어에서 이 동작을 볼 수 있습니다.

**2.4에서 지원됨**

버전 2.4에서는 다음 기능을 사용할 수 있었습니다.

* **MP3 오디오 재생**

   이 릴리스는 MSE(Media Source Extensions)가 설치된 브라우저 및 Safari 비디오 태그와 함께 MP3 오디오 재생을 지원합니다.

* **MP4 비디오 재생**

   지원되는 기능은 다음과 같습니다.

   * 단일 스트림 재생
   * 광고 행동 및 추적 기능을 갖춘 프리롤 및 포스트롤 MP4 광고
   * 광고 행동 및 추적 기능이 있는 프리롤 및 포스트롤 HLS 광고
   * 광고 행동 및 추적 기능이 있는 프리롤 및 포스트롤 DASH 광고

## 지원되는 플랫폼 {#supported-platforms}

브라우저 TVSDK는 실행해야 하는 플랫폼 및 소프트웨어 수준에 대한 특정 요구 사항을 가지고 있습니다. 다음과 같은 플랫폼 및 소프트웨어 수준이 지원됩니다.

### 데스크톱 구성 {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### 모바일 웹 구성 {#mobile-web-configurations}

* Android 4.4

   * 기본 브라우저
   * Chrome 33+

* Android 5.0

   * 기본 브라우저
   * Chrome 33+

* Android 6.0

   * ・ Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast(2세대;for DASH playback only)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>기술</strong> </p> </td> 
   <td><p><strong>브라우저 TVSDK 비디오 태그</strong><sup>1</sup></p> </td> 
   <td><p><strong>브라우저 TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>기본 기술</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>비디오 태그</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS 및 대시</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>비디오 태그</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS 및 대시</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS 및 대시</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, 대시</p> </td> 
   <td><p>MP4 및 HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## 기능 매트릭스 {#feature-matrix}

다음은 이번 릴리스에서 지원되고 지원되지 않는 기능 목록입니다.

* *MP3 오디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 핵심 Ad Insertion*

>[!NOTE]
>
>*아래의 기능 매트릭스 표에서 &#39;Y&#39;는 이 기능이 현재 릴리스에서 지원됨을 의미합니다.*

### MP3 오디오 기능 {#mp-audio-features}

**표 1:코어 재생{#table-core-playback}**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP3 VOD | 일반 재생(재생, 일시 중지, 검색) | 지원되지 않음 | Y | Y |

1 브라우저 TVSDK 비디오 태그는 스트리밍 및 DRM을 지원하지 않습니다. 코덱과 컨테이너 지원은 모든 브라우저에서 동일하지 않습니다.

2 버전 41 이전 버전의 경우 Firefox가 기본적으로 Flash Player으로 설정됩니다.

### MP4 오디오 기능 {#mp-audio-features-1}

**표 2:코어 재생**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP4 VOD | 일반 재생(재생, 일시 중지, 검색) | 지원되지 않음 | Y | Y |

**표 3:핵심 Ad Insertion**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 프리롤(MP4) | 지원되지 않음 | Y | Y |
| Ad Insertion | MP4 VOD | 포스트롤(MP4) | 지원되지 않음 | Y | Y |

HLS 또는 DASH 기능 지원에 대한 자세한 내용은 아래를 참조하십시오.

## HLS 기능 매트릭스 {#hls-feature-matrix}

다음은 브라우저 TVSDK의 HLS 기능에 대한 기능 매트릭스입니다.

* *HLS Core 재생*
* *HLS 고급 재생 기능*
* *HLS 컨텐츠 보호 기능*
* *HLS 코어 광고 삽입 기능*
* *HLS 고급 광고 삽입 기능*
* *HLS 통합*

>[!NOTE]
>
>*아래의 기능 매트릭스 표에서 &#39;Y&#39;는 이 기능이 현재 릴리스에서 지원됨을 의미합니다.*

### HLS 기능 {#hls-features}

지원되는 기능은 다음과 같습니다.

**표 4:HLS Core 재생**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>일반 재생(재생, 일시 정지, 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>일반 재생(재생, 일시 정지 및 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>적응형 비트 전송률</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>608/708 캡션</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>VOD만</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>매니페스트 장애 조치(Manifest Failover)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>고급 페일오버</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>QoS 및 플레이어 알림</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>제한된 QoS 지원</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>쿠키 헤더 지원</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>버퍼 컨트롤 매개 변수 설정</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>응용 설정</p> <p>비트 전송률 제어</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>사용자 지정 태그</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td>지연 바인딩 오디오</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>302 리디렉션</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 5:HLS 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오프셋 재생</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오디오 전용 재생</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>부드러운 트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>ID3 구문 분석</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>끊김 마커 지원</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>토큰화된 스트림</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>청구</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 6:HLS 컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>샘플-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe 액세스</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 7:HLS 코어 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>프리롤(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>중간 롤(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>포스트롤(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>광고 해상도 및 행동</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>기본 광고 정책</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>크리에이티브 재패키징(MP4에서 HLS로)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 8:HLS 고급 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>광고 전용</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>타깃팅 매개 변수</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>사용자 지정 매개 변수</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>맞춤형 광고 정책</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>레이지 광고 로딩</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>컴패니언 광고, 배너 광고, 클릭 가능한 광고</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 9:HLS 통합{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>통합</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>Adobe Analytics VHL 통합</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## DASH 기능 매트릭스 {#dash-feature-matrix}

다음은 브라우저 TVSDK의 DASH 기능에 대한 기능 매트릭스입니다.

・ *DASH 코어 재생 기능*

・ *DASH 고급 재생 기능*

・ *DASH 컨텐츠 보호 기능*

・ *DASH 코어 광고 삽입 기능*

・ *DASH 고급 광고 삽입 기능*

・ *DASH 통합*

>[!NOTE]
>
>아래의 기능 매트릭스 표에서 Y는 현재 릴리스에서 기능이 지원됨을 의미합니다.

### DASH 기능 {#dash-features}

지원되는 기능은 다음과 같습니다.

**표 10:DASH Core 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>일반 재생(재생, 일시 정지, 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>일반 재생(재생, 일시 정지 및 검색)</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>적응형 비트 전송률</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>608/708 캡션</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>장애 조치</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>QoS 및 플레이어 알림</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>쿠키 헤더 지원</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>버퍼 컨트롤 매개 변수 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>적응형 비트 전송률 컨트롤 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>사용자 지정 태그(EventStream)</p> </td> 
   <td><p>VOD 전용(인라인)</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>늦게 바인딩된 오디오</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>302 리디렉션</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 11:DASH 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오프셋 재생</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오디오 전용 재생</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>부드러운 트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>ID3 구문 분석</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>다중 기간 지원</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>토큰화된 스트림</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>청구</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 12:DASH 컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>샘플-AES</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Chrome, Firefox 47 이상 및 Chromecast의 위드라인</p> <p>・ Windows 8.1 및 Edge에서 Internet Explorer에서 재생</p> <p>・ Windows Firefox용 Primetime DRM(비디오 전용)</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 13:DASH 코어 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>프리롤(MP4/DASH)</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>중간 롤(DASH)</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>포스트롤(MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>광고 해상도 및 행동</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>기본 광고 정책</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>크리에이티브 재패키징(MP4에서 DASH)</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 14:DASH 고급 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>광고 전용</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>타깃팅 매개 변수</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>사용자 지정 매개 변수</p> </td> 
   <td><p>VOD만</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>맞춤형 광고 정책</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>레이지 광고 로딩</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>컴패니언 광고, 배너 광고, 클릭 가능한 광고</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 15:대시 통합**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5:FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>통합</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>Adobe Analytics VHL 통합</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 문제 수정 {#issues-fixed}

**2.4.12 업데이트(빌드 204)에서 해결된 문제**

다음 문제는 브라우저 TVSDK 버전 2.4.12 업데이트(빌드 204)에서 해결되었습니다.

・ 오디오가 음소거되어 있는 경우 TVSDK가 iOS 장치에서 자동 비디오 재생을 허용해야 합니다.****

・ DASH 라이브 스트림이 재생된 후 DRM으로 보호된 DASH 스트림을 재생할 때 **21465**- 오류 키 시스템 액세스 거부됨 이 수신됩니다.

・ **21442**- 프리롤 광고가 사용자 제스처로 재생된 후 iOS 웹에서 내용 자동 재생 활성화

・ **21240**- Auditude/VMAP에서 파싱된 VPAID 광고를 필터링하기 위해 제공된 API.

**버전 2.4.11에서 해결된 문제**

Browser TVSDK version 2.4.11에서 다음 문제가 해결되었습니다.

**핵심 재생 기능:**

・ **19192**:이제 TVSDK에서 TextFormat:bottomInset 및 TextFormat:safeArea를 구현합니다. 이러한 향상된 기능 때문에 컨트롤 막대가 화면에 표시되면 닫힌 캡션을 다시 배치할 수 있습니다.

・ **21009**:자막이 새로 나타날 때까지 중단이 있을 경우 숨겨진 캡션이 화면에 계속 나타납니다.

・ **21141**:세그먼트 첨부 중 경합 조건으로 인해 뒤로 검색이 거부됩니다.

・ **21142**:플레이어가 INITIALIZED 상태일 때 검색 가능한 재생 범위를 사용할 수 있도록 합니다. 이러한 변경 사항으로 인해 이제 위치에서 세션을 시작할 수 있습니다.

・ **21363**:DASH 스트림에 대한 광고 삽입 후 608/708 자막이 동기화되지 않습니다.

**광고 삽입 기능:**

・ **21179**:이제 ad.primaryAsset.adParameters 속성을 올바르게 설정하여 VOD 컨텐츠가 포함된 중롤 관련 문제(긴 일시 중지, 검정 프레임)가 해결되었습니다.

・ **21257**:MP4가 유효한 MIME 유형이 아니며 크리에이티브 재패키징 기능이 활성화된 경우 비트가 가장 높은 MP4 파일을 트랜스코딩하도록 선택합니다.

・ **21361**:이제 TVSDK는 추가적인 표준화 규칙을 지원하기 위해 VAST 응답의 광고 시스템 및 크리에이티브 ID를 크리에이티브 패키징 요청의 쿼리 매개 변수로 전달합니다.

**버전 2.4.10에서 해결된 문제**

Browser TVSDK version 2.4.10에서 다음 문제가 해결되었습니다.

**핵심 재생 기능:**

・ **21060**:불연속성이 포함된 HLS 스트림과 함께 잘못된 코덱을 throw했으며 ISO BMFF 상자가 스트림 끝까지 실행됩니다.

・ **21045**:재생 목록의 첫 번째 비디오 재생이 완료된 후 iOS에서 자동 재생이 작동하지 않습니다.

・ **20975**:Chrome 브라우저의 QoS 제공자가 프레임 속도를 NaN으로 반환합니다.

・ **20823**:데이터가 없는 세그먼트에서 발생하는 지원되지 않는 코덱입니다.

・ **20769**:이제 SDK는 ABR 정책을 기반으로 즉시 전환하지 않고 현재 비트 전송률을 검색 시 시작합니다.

・ **20031**:IE11(Windows 8.1)의 세로 모드에서는 비디오 화면이 작아집니다. 컨텐츠 보호 기능:

・ **19316**:HLS AES-128 스트림의 경우 암호 해독에 실패한 세그먼트 건너뛰기

**버전 2.4.9에서 해결된 문제**

Browser TVSDK version 2.4.9에서 다음 문제가 해결되었습니다.

**핵심 재생 기능:**

・ **13407**:재생 중에 Firefox &quot;ontimeupdate&quot; 이벤트 전송을 중지하면 DASH 스트림이 중단될 수 있습니다.

・ **16380**:MSE를 통해 시작 시간이 일치하지 않는 세그먼트의 다중 오디오 비디오 컨텐츠 재생 동안 표현 간 오디오 동기화 오류가 ABR 스위치에서 누적되어 오류가 발생합니다(Chromium 문제 #663686).

・ **17985**:Firefox 브라우저에서 특정 ISO-BMFF 스트림을 재생하면 재생이 멈춥니다(Firefox 문제 번호 1342913). 이 문제는 Firefox v53 이후 수정되었습니다.

・ **19141**:처리할 수 없음(약속됨) 참조오류:너비가 정의되지 않았습니다.

・ **18997, 19299**:세그먼트 경계에서 비디오 깜박임 문제 SDK가 마지막 샘플의 컴포지션 시간 오프셋을 올바르게 계산하지 않았기 때문에 이러한 문제가 발생했습니다.

・ **19780**:Firefox v53에서 HLS 컨텐츠 및 HLS 광고 재생이 시작되지 않습니다(Firefox 문제 번호 354653).

・ **20046**:프로그램 날짜 시간은 시간 메타데이터 개체로 수신될 때 값이 아닌 키로 수신됩니다.

・ **20047**:useDefaultResizeHandler가 Flash 폴백을 사용하여 오류를 표시합니다.

・ **20179**:Flash Player v25.0.0.171에서 Flash 폴백이 작동하지 않습니다.

・ **20293**:Firefox는 특정 HLS 스트림에 대한 버퍼링 데이터를 중지하여 실행을 중단합니다.

・ **20626**:Player는 지속 시간이 0인 비디오 샘플의 잘못된 처리 때문에 Chrome에서 미디어 디코드 오류를 발생시킵니다.

・ **20078**:브라우저 오류 &#39;QuotaExceeded&#39;에서 재생을 중단합니다.

・ **18639**:HLS Live 스트림 608 CC 텍스트의 맞춤법이 틀린 경우도 있습니다.

・ **20028**:ClosedCaptions 크기 매개 변수는 글꼴 크기를 변경하지 않습니다.

・ **20613**:자막 상자가 서로 겹쳐서 알아보기 어렵게 만듭니다.

**핵심 Ad Insertion(CSAI) 기능:**

・ **20043**:여러 광고 및 타사 리디렉션이 포함된 광고 노출 및 광고 추적 호출이 없습니다.

・ **20044**:크리에이티브 재패키징을 사용하는 경우 광고 중단의 모든 광고를 성공적으로 다시 패키지해야 합니다. 그렇지 않으면 광고 중단이 완전히 무시됩니다.

・ **20097**:광고 매니페스트를 사용할 수 없는 경우 20초 동안 기다릴 필요 없이 광고 재생을 건너뛰고 주요 컨텐츠가 바로 재개됩니다.

**버전 2.4.8 업데이트(빌드 6002)에서 해결된 문제**

다음 문제는 브라우저 TVSDK 버전 2.4.8 업데이트(빌드 6002)에서 해결되었습니다.

・ MSE 소스 버퍼의 내부 간격으로 인해 **14126:** Firefox에서 재생을 중지할 수 있습니다(문제 번호 1316024). 재생을 다시 시작하려면 검색

・ **19608:** Auditude VMAP 응답에서 시간 오프셋 값을 유지하도록 수정

・ **19635:** Windows 10에서 Internet Explorer 11의 비디오 정지 수정

・ **19761:** HLS와 관련된 ABR 문제에 대한 수정 사항

・ **19780:** Mozilla Firefox v53에서 손상된 HLS 컨텐츠로 광고 재생을 수정합니다.

・ **19877 및 19744:** 검색 작업 후 비트 전송률을 선택할 때 발생하는 불일치 문제가 해결됩니다. 이제 시중에서 비트 전송률을 선택하면 현재 비트 전송률과 시작 시 비트 전송률이 낮아집니다.

・ **19881:** 검색을 3-4회 수행한 후 재생 정지 및 버퍼링 오버레이가 무한 시간 동안 나타납니다.

・ **19884:** Chrome 59 베타 확인된 미디어 경로(VMP) 요구 사항 준수 확인 bTVSDK는 Chrome 59 Beta에서 Widevine DRM 컨텐츠를 재생할 수 있었습니다.

・ **19916:** UI-Framework에서 DRM 재생이 손상되었습니다. 메타데이터에 정책이 없는 경우에도 acquireLicense를 호출합니다.

**버전 2.4.8에서 해결된 문제**

Browser TVSDK 2.4.8 릴리스에서 다음 문제가 해결되었습니다.

・ **10075**:타임라인을 앞서서 검색하는 경우 Firefox 및 Chrome에서 재생 완료 이벤트가 수신되지 않고 Firefox에서 검색 이벤트가 수신되지 않았습니다.

・ **15775**:Windows 8.1 Internet Explorer에서 수신된 이벤트 재생 완료

・ **17306**:SSAI 스트림의 경우 재생이 지원됩니다. 연결된 광고 추적은 지원되지 않습니다.

・ **19142**:때때로 되감기는 비디오 플레이어가 버퍼링 상태로 영원히 남도록 합니다.

・ **19218**:광고 마커는 UI 프레임워크를 통해 사용할 수 없습니다.

・ **19219**:UI 프레임워크를 통해서는 광고 재생만 작동하지 않습니다.

・ **19222**:재생 목록에 대해 AES-128 키가 요청되고 이후 요청이 캐시에서 제공됩니다. 이전에는 각 세그먼트에 대해 요청을 받았습니다.

・ **19597**:&quot;확인할 수 없는 유형 오류:정의되지 않은&quot; 속성의 &#39;log&#39; 속성을 읽을 수 없습니다. Chrome 카나리아 빌드가 있습니다.

・ **19605**:flash 폴백 모드에서는 adRequestDomain을 사용할 수 없었습니다.

・ **19608**:HLS 라이브 스트림에 대해 VMAP 광고가 삽입되지 않았습니다. 이제 SDK는 큐 마커를 고려하며 VMAP 응답에서 시간 오프셋 값을 사용하지 않습니다.

・ **19637**:광고 재생만 시행되면 광고 끝에 스크립트 오류가 발생합니다.

・ **19732**:404 오류가 발생하여 CRS 재생 목록 요청이 실패했습니다. 이제 Browser TVSDK의 1401 및 1403 요청이 업데이트되어 이를 처리합니다.

・ **19762**:토큰 유효성과 관계없이 유효한 라이선스가 반환되기 때문에 setAuthenticationToken 이전에 호출된 acquireLicense가 사용되었습니다. 이 문제가 해결되었으며 acquireLicense는 setAuthenticationToken 응답 후에만 호출됩니다.

**버전 2.4.7에서 해결된 문제**

버전 2.4.7에서는 다음 문제가 해결되었습니다.

・ **8397**:세그먼트가 키 프레임으로 시작하지 않으면 Adobe Media Server를 통해 생성된 HLS 라이브 스트림이 재생되지 않을 수 있습니다.

・ **13606**:Chrome 브라우저의 HLS 스트림에 대해 다중 검색 관련 문제가 해결되었습니다.

・ **14807**:Chrome 브라우저의 경우 play() 직후 검색 또는 일시 중지가 트리거되면 DOMException 오류 시 재생이 중지될 수 있습니다.play() 요청이 호출로 중단되었습니다..(Chromium 문제 번호 593273).

・ **19085**:볼륨, abrControlParameters 및 ccStyle과 같은 MediaPlayer 매개 변수는 플레이어 재설정 시 기본값으로 설정되지 않습니다.

**버전 2.4.6에서 해결된 문제**

버전 2.4.6에서 다음 문제가 해결되었습니다.

・ **18093**:Flash 폴백 모드에서 Flash Player 버전 24를 사용하면 구독된 태그 옆에 있는 태그에 대한 TimedMetadata가 반환됩니다.

**버전 2.4.4에서 해결된 문제**

버전 2.4.4에서는 다음 문제가 해결되었습니다.

・ **8711**:MSE에서는 608/708 캡션이 기본적으로 균등하게 정렬됩니다.

・ **13934**:HLS 라이브 스트림을 사용하여 재생하는 경우 광고에 대한 ABR 설정을 적용할 수 없습니다.

・ **14079**:DVR 창이 낮은 HLS Live 스트림의 수명은 네트워크 지연 문제로 인해 재생이 지연될 수 있으므로 실패할 수 있습니다. 재생을 다시 시작하려면 라이브 포인트를 클릭합니다.

・ **15037**:플레이어 UI 프레임워크와 함께 제공된 샘플은 Windows 7의 Microsoft Internet Explorer 10에서 작동하지 않습니다.

・ **15913**:크롬에서 HLS VOD 스트림의 경우 매니페스트 응답이 304가 수정되지 않은 경우 스트림이 재생되지 않습니다. Chrome v55(Chromium 문제 633696) 이후 수정되었습니다.

・ **16103**:Android Chrome의 경우 낮은 대역폭 조건에서 Uncaught TypeError가 발생하여 재생을 중지할 수 있습니다.정의되지 않은 오류의 &#39;programDateTime&#39; 속성을 읽을 수 없습니다.

・ **16265**:HLS VOD 및 라이브 스트림의 경우, 불연속적 검색 기능은 작동하지 않습니다.

・ **16709**:PDT 및 중단 마커로 HLS 라이브 스트림을 다시 시작하면 플레이어가 버퍼링에 고정될 수 있습니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

Browser TVSDK의 제한 사항과 알려진 문제는 아래에 명시되어 있습니다.

**표 16:핵심 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생 전용)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>일반 재생(재생, 일시 중지, 검색)</td> 
   <td><p>・ HLS 이외의 미디어 포맷은 지원되지 않습니다.</p> <p>8799:Flash 대비책은 혼합 컨텐트를 처리하지 않으므로, 따라서 컨텐츠, 광고 및 기타 URL이 혼합 컨텐츠(보안 및 비보안 컨텐츠)로 연결되지 않도록 보장할 필요가 있습니다.</p> <p>・ 19271:UI 프레임워크를 통한 다중 보기 재생은 Flash 폴백 모드에서 지원되지 않습니다.</p> <p>・ Windows 7의 Microsoft Internet Explorer 8 및 9에서는 이러한 버전이 SDK에서 지원되지 않으므로 Flash 폴백이 작동하지 않습니다.</p> <p>・ 20262:Flash 폴백은 타깃팅 정보 목록에 사용자 지정 매개 변수를 추가합니다. 또한 Flash 및 MSE의 경우 사용자 지정 매개 변수의 우선 순위 순서가 다릅니다.</p> <p>・ 20653: Creators Update를 사용하는 Win10에서 브라우저 TVSDK Flash 폴백이 작동하지 않습니다.</p> <p>・ Flash 폴백이 Flash Player 버전 23 이상에서 작동합니다.</p> <p>・ 20087 - Chrome 59 베타(베타 포함)</p> <p>Flash 25.0.0.171</p> <p>베타(기본값), HLS 재생이 Flash 폴백 모드에서 작동하지 않습니다. 카나리아에서는 잘 작동합니다.</p> </td> 
   <td><p>・ 12563:오디오 코덱이 포함된 대시 스트림은 MPD에서 지원되지 않는 오디오 코덱으로 인해 Firefox에서 재생되지 않습니다. 오디오 코덱인 mp4a.40.2가 지원됩니다.</p> <p>15029:UI-Framework의 multiView에서 비디오 간을 전환하는 동안 재생/일시 정지 단추가 그에 따라 업데이트되지 않습니다.</p> <p>・ 16034: Windows 8.1 IE에서 reset()을 호출하면 알 수 없는 MIME 유형 오류가 발생합니다. 재생을 다시 시작하려면 미디어를 다시 로드하십시오.</p> <p>・ 18235:광고를 통한 DASH VOD 스트림에서 특정 검색 문제가 관찰됩니다.</p> <p>・ 18727:MSE에 대해 오류 API가 지원되지 않음</p> <p>18750년:SDK 및 UI 프레임워크와 UI 프레임워크 모두에 대해 상태 변경 이벤트가 잘못된 경우가 있을 수 있으며, 리소스가 로드된 후 추가된 이벤트 리스너에 대해 유휴 및 초기화 상태 변경 이벤트가 누락될 수 있습니다.</p> <p>・ 18889:MediaPlayer가 ERROR 상태인 경우 보기 개체가 반환되지 않습니다.</p> <p>・ 19039:AdobePSDK인 경우 MediaPlayer. seekToLocal()은 EOF보다 큰 값과 함께 사용되지만 MSE의 경우 처음 재생됩니다.</p> <p>・ 19049:재생하는 동안 비디오가 차단된 경우 Chrome, IE, Firefox의 Flash Player에 대해 보고된 오류 상태가 없습니다.</p> <p>・ 17205:오디오가 계속 재생되는 동안 비디오 재생이 고정 스트림을 몇 시간 동안 정지합니다(Chromium 문제# 64033).</p> <p>・ 12308:composition_time_offset이 지정된 대시 스트림에는 timeStampOffset이 Chrome 브라우저에 적용되어 음성 디코드 시간이 발생하므로 MEDIA_ERR_SRC_NOT_ SUPPORTED 오류(Chromium 문제 #398141)가 발생할 수 있습니다.</p> <p>・ 14126:MSE 소스 버퍼의 내부 간격으로 인해 Firefox(문제 번호 1316024)에서 재생을 중지할 수 있습니다. 재생을 다시 시작하려면 검색을 시도하십시오.</p> <p>・ 19115:MS Edge 및 IE 11(Win 8.1 및 10)은 CORS 리디렉션에서 Origin을 null로 설정하지 않으며 헤더가 Null이 아니므로 재생을 위한 오류가 발생하지 않습니다.</p> <p>・ 19861: 이미 재생된 미디어의 소스 버퍼에 동작 추가 문제가 해결되었습니다. Chrome은 moov를 포함한 추가된 조각을 거부하여 후속 디코딩 오류가 발생합니다. (Chromium 문제 #735335)</p> <p>19921년:버퍼링을 성공적으로 수행하더라도 특정 HLS 컨텐츠에 대해 재생을 중단합니다(Chromium 문제 #713540).</p> <p>・ 20444: IE와 Edge에서 버퍼링된 범위의 끝을 찾다 재생이 지연될 수 있습니다.</p> <p>・ 20511:경우에 따라 광고 포함 또는 없는 HLS 스트림에 대해 거부 찾기를 확인할 수 있습니다.</p> <p>・ 20743:Windows 10 Chrome에서 HLS 라이브 스트림은 MP4 프리롤 재생 전에 몇 초 동안 재생됩니다.</p> <p>・ 21043:메타데이터가 없어서 초기 로드에서 비디오 차원이 정확하지 않을 수 있습니다.</p> <p>・ 21115:재생 목록의 비디오에 프리롤 광고를 사용할 수 있는 경우 재생을 시작하려면 Android 사용자 제스처가 필요합니다.</p> <p>・ HLS Live에서는 타임스탬프 롤오버를 지원하지 않습니다.</p> <p>・ AAC-SSR 오디오가 지원되지 않습니다.</p> <p>오디오 코덱의 AC3 및 향상된 AC3는 지원되지 않습니다.</p> <p>・ 타임스탬프 불연속성이 있는 스트림의 경우, 끊김 마커가 없는 경우</p> <p>・ 재생 중에 이동 때문에 잘못된 검색 결과가 나타날 수 있습니다.</p> <p>・ 컨텐츠 지속 시간과 재생 시간이 일치하지 않을 수 있습니다.</p> <p>・ 모든 표현 및 표현물의 불연속성이 다른 지식으로 대응하면 동기화 및 중단 문제가 발생할 수 있습니다.</p> <p>・ 캡션 및 WebVTT은 스트림 끝에 표시되지 않을 수 있습니다.</p> <p>・ 타임스탬프 이동 시 오디오 코덱의 변경이 지원되지 않습니다.</p> <p>・ 광고 삽입이 지원되지 않습니다.</p> <p>・ 빠른 정방향 트릭 모드를 사용하면 Win 8.1 IE 11에서 재생 루프가 발생할 수 있습니다(MS 문제 번호 12446268).</p> <p>대시:</p> <p>・ 실시간 스트림의 경우 - 동적 유형의 라이브 프로필이 지원됩니다.</p> <p>・ VoD 스트림의 경우 - 정적 유형의 라이브 프로필이 지원됩니다.</p> <p>VoD 스트림의 경우 - 광고 워크플로우에 대해 온디맨드 프로필이 인증되지 않습니다.</p> </td> 
   <td><p>・ DASH 라이브 및 DASH Video on Demand 스트림은 지원되지 않습니다.</p> <p>・ PIP(Picture in Picture) 비디오 재생은 전체 화면 모드에서 iOS에서 지원되지 않습니다.</p> <p>Safari(비디오 태그) 확장 시 올바른 콘텐츠 형식 헤더가 없는 매니페스트(less manifest)가 작동하지 않습니다.</p> </td> 
   <td><p>・ 발신자 앱의 applicationID는 수신자의 URL을 사용자 지정 수신기 앱으로 등록할 때 생성되는 것과 같아야 합니다.</p> <p>・ DASH 워크플로우에 대한 참조 플레이어 인증 UI 프레임워크가 인증되지 않았습니다.</p> <p>지원되는 미디어 코덱의 목록은 <a href="https://developers.google.com/cast/docs/media"><em>여기</em></a>를 참조하십시오.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>일반 재생(재생, 일시 중지, 검색)</td> 
   <td> </td> 
   <td>18098년:HLS LBA FER 스트림에서 특정 검색 문제가 관찰됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>적응형 비트 전송률</td> 
   <td><p>・ 20079:버퍼링된 범위 내의 검색 시 버퍼링된 다시 쓰기</p> <p>20080년:Flash ABR 동작이 MSE와 일치하지 않습니다.</p> </td> 
   <td><p>・ ABR 스트림의 오디오 전용 폴백 변형이 버퍼 관련 제한으로 인해 무시됩니다.</p> <p>・ 12289:ABR 컨트롤 매개 변수는 혼합되지 않은 HLS/DASH 스트림의 경우 오디오에 적용되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>608/708 캡션</td> 
   <td> </td> 
   <td><p>・ 7810:Android 4.4.4 Chrome에서는 플레이어에서 사용하는 기본 CSS 글꼴 모음을 지원하지 않는 것 같습니다. 따라서 글꼴 스타일 변경 기능이 작동하지 않습니다.</p> <p>・ 608 캡션의 경우 CC 채널을 변경할 수 없습니다.</p> <p>・ 608 캡션에는 고급 스타일 기능이 지원되지 않습니다.</p> <p>포함된 캡션(608/708), 접근성 태그를 통해 표시되는 캡션이 지원됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206:WebVTT 파일의 영역 태그는 캡션을 표시할 때 플레이어에서 무시됩니다.</p> <p>・ 대시:조각화된 /세그먼트화된 VTT 파일은 지원되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>매니페스트 장애 조치</td> 
   <td>21056:Flash 폴백이 있는 경우 기본 스트림이 재생 중에 404 오류를 반환하는 경우 라이브 스트림에 대해 장애 조치가 발생하지 않습니다.</td> 
   <td>매니페스트 장애 조치(failover)는 콘텐츠에만 적용되며 광고는 해당되지 않습니다.</td> 
   <td>Safari에서는 HTTP 오류 코드 404에 대해서만 재생 목록 장애 조치가 작동합니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>고급 페일오버</td> 
   <td> </td> 
   <td><p>・ 세그먼트 장애 조치(failover)는 사용할 수 없는 세그먼트 건너뛰기와 계속 재생을 지원하지 않습니다.</p> <p>20533:재생 목록에 누락된 세그먼트는 불연속성 세그먼트로 처리되어야 하며 재생 가능한 다음 세그먼트에서 다시 시작해야 합니다.</p> <p>21267:장애 조치(failover)로 인해 스트림 전환이 가능하므로 이전 세그먼트를 다운로드할 수 있습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>QoS 및 플레이어 알림</td> 
   <td>21129:Flash 폴백이 있는 경우 프레임 속도를 사용할 수 없습니다.</td> 
   <td><p>・ 11170:</p> <p>Timed_Event는 Flash 폴백이 있는 브라우저 TVSDK와 달리 MSE가 있는 브라우저 TVSDK에서는 사용할 수 없습니다.</p> <p>21129:라이브 스트림에 대해 프레임 속도가 계산되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>쿠키 헤더 지원</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials 플래그 및 쿠키 헤더는 Safari에서 지원되지 않습니다.</p> <p>21051:Safari에서 쿠키를 허용하려면 [환경 설정] &gt; [개인 정보]에서 "쿠키 및 웹 사이트 데이터" 설정을 활성화합니다.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>사용자 지정 태그</td> 
   <td>14763:# 이외의 사용자 지정 태그는 지원되지 않아야 합니다. 현재 TimedMetadata 개체는 Flash 폴백 중 이러한 태그에 대해 만들어지고 보고됩니다.</td> 
   <td>인밴드 사용자 지정 태그가 있는 스트림은 인증되지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>오디오 지연 바인딩</td> 
   <td> </td> 
   <td><p>・ HLS 라이브 LBA 스트림에서는 광고 삽입이 지원되지 않습니다.</p> <p>・ 17273:장애 조치 시 HLS VOD LBA 스트림은 기본 변환으로 전환되며 마지막으로 선택한 버전으로 다시 전환할 수 없습니다.</p> <p>・ 20251:HLS Live LBA 스트림이 검색 중 정지될 수 있습니다.</p> <p>・ 20497:HLS LBA 무출력 스트림에 오디오 또는 비디오 프레임이 스트림 끝에 도달하면 플레이어가 버퍼링 상태로 유지됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>302 리디렉션</td> 
   <td> </td> 
   <td><p>15787:302년</p> <p>XMLHttpRequest 개체의 responseURL 속성을 지원하지 않으므로 windows Edge 및 IE 브라우저에서는 리디렉션 최적화가 지원되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 17:고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td>컨텐츠 유형</td> 
   <td>기능</td> 
   <td>Flash</td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생 전용)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>오프셋 재생</td> 
   <td><p>특정 오프셋 값에서 재생을 시작하는 것은 MP4 콘텐츠를 지원하지 않습니다.</p> </td> 
   <td>20492년:오프셋 앞의 중간 롤 광고는 컨텐츠가 오프셋 값에서 다시 시작되기 전에 재생됩니다.</td> 
   <td>오프셋 기능을 사용한 재생은 iOS에서 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>트릭 플레이</td> 
   <td>iFrame 변환이 없는 스트림에는 부드러운 트릭이 작동하지 않습니다.</td> 
   <td><p>・ Trick Play 어댑터는 Firefox 및 Internet Explorer에서 지원되지 않으므로 이러한 브라우저에서는 역 트릭 모드를 사용할 수 없습니다.</p> <p>・ 광고와 함께 콘텐츠를 재생하는 경우 트릭을 사용할 수 없습니다.</p> <p>・ 10435:DASH 재생 중에 Internet Explorer에서 정방향 트릭 재생 시 비디오가 멈춥니다(Win 8.1).</p> <p>간헐적으로 이러한 문제는 trick play 적응하지 않고 비디오 요소 playbackRate 속성을 사용하기 때문에 발생합니다.</p> <p>14182:Chrome 브라우저에서 되감기 동안 검색 이벤트가 수신되지 않을 수 있으므로 트릭 모드가 작동하지 않는 경우가 있습니다.</p> <p>・ 14942:비트릭 재생 스트림의 경우에도 Android용 Chrome에서 재생 속도를 설정할 수 있지만 설정이 적용되지 않고 정상적인 속도로 재생됩니다.</p> <p>・ 17308:Seek는 Trickplay 모드에서 작동하지 않습니다.</p> <p>・ 17309:크롬 브라우저에서 역 트릭 모드는 2초 이상 유지할 수 없습니다.</p> <p>19272년:트릭 플레이는 DASH 스트림의 경우 Windows 10 Edge 브라우저의 버퍼링에서 복구되지 않을 수 있습니다.</p> </td> 
   <td>되감기 트릭 모드는 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>ID3 구문 분석</td> 
   <td>20346:ID3 프레임의 텍스트 인코딩 바이트도 SDK에서 반환해야 합니다.</td> 
   <td><p>ADTS(오디오 데이터 전송 스트림)에서 사용할 수 있는 ID3 태그는 SDK에서 무시됩니다.</p> <p>・ 12378:ID3 시간 메타데이터는 MSE를 지원하는 Flash 및 브라우저에서 서로 다른 시간에 구문 분석되므로 참조 플레이어 타임라인에서의 표시 동작도 다릅니다.</p> <p>・ 19247:ID3 구문 분석은 UI 프레임워크에서 지원되지 않습니다.</p> </td> 
   <td><p>・ 20323:AAC 세그먼트의 첫 번째 샘플의 타임스탬프를 표시하는 데 사용되는 PRIV ID3 태그가 Safari에 의해 구문 분석되지 않습니다(Safari 문제 #3242273).</p> <p>・ 20350:특정 장치(MAC OS X 10.1, iPad10 포함)에서 Safari는 트릭 모드에서 큐 변경 이벤트를 제공하지 않으므로 ID3 프레임이 수신되지 않습니다. (Safari 문제 #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>끊김 마커 지원</td> 
   <td> </td> 
   <td><p>・ 클라이언트측 광고 삽입은 불연속성이 포함된 HLS 스트림에서 지원되지 않습니다.</p> <p>・ HLS 스트림의 불연속성에서는 오디오 코덱을 변경할 수 없습니다.</p> <p>・ 불연속 마커가 있는 HLS 스트림에는 오디오 트랙 스위치가 지원되지 않음</p> </td> 
   <td>불연속 시퀀스 번호는 Safari에서 재생하기 위해 불연속성이 있는 HLS 스트림의 요구 사항입니다.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 18:컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생 전용)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>바이트 범위는 AES-128로 암호화된 콘텐츠에서 지원되지 않습니다.</td> 
   <td>12324:IV 태그가 지정되지 않은 경우 Safari에서 HLS AES-128로 암호화된 스트림이 재생되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660:HTML5 플레이어에서 만료된 PlayReady 암호화된 대시 내용에 대한 내부 서버 오류가 발생합니다.</p> <p>・ 16720:마침표 태그의 시작 속성이 없으면 DASH DRM 암호화된 내용이 작동하지 않습니다.</p> <p>・ 18589:Xlink를 통해 DRM으로 보호된 Dash VoD 다중 기간 스트림에서는 재생이 지원되지 않습니다.</p> <p>・ 18653:여러 개의 키가 있는 Widevine MultiPeriod 컨텐츠의 재생은 첫 번째 시간에 중단되며 다음 기간으로 전환할 수 없습니다.</p> <p>・ 18656:재생 가능한 다중 기간 스트림. 다른 키로 암호화되므로 재생하지 않아도 됩니다.</p> <p>대쉬용 Playready 2.0이 인증되지 않았습니다.</p> <p> </p> <p> </p> </td> 
   <td>12602:Safari의 HTML5 플레이어에서 HLS Fairplay DRM 메타데이터를 반복적으로 새로 고칩니다.</td> 
   <td><p>Bento4를 통해 패키지화된 DASH Widevine DRM 내용을 재생할 수 있습니다. Offline Packager 및 Shaka Packager를 통해 패키지된 컨텐츠는 재생되지 않습니다. DASH PlayReady DRM은 지원되지 않습니다.</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 19:핵심 Ad Insertion 기능(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생 전용)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>이전/중간/이후</td> 
   <td> </td> 
   <td><p>・ HLS 라이브 컨텐츠가 있는 프리롤 광고는 듀얼 플레이어 모드로 재생됩니다.</p> <p>・ HLS 컨텐츠 및 HLS 광고가 있는 대시 광고는 지원되지 않습니다.</p> <p>・ 19002:MSE adBreak가 있는 HTML5 플레이어 insertionType은 삽입된 클라이언트 또는 삽입된 서버 등 올바른 삽입 유형을 나타내기 위해 올바른 값을 반환하지 않습니다.</p> <p>7794:기본 컨트롤 막대가 전체 화면 모드에서 표시되는 모바일 장치(iOS, Chrome 33 이하 또는 기본 브라우저가 설치된 Android)에서는 광고 재생 시 검색 막대와 빨리 감기 단추를 사용할 수 있습니다.</p> <p>・ 11048:미디어 소스 익스텐션의 경우 광고를 HLS 라이브 컨텐츠로 전환할 수 없습니다.</p> <p>・ 16083:Android 4.4 Chrome v52에서 HLS 컨텐츠가 있는 HLS 광고가 재생을 중단하면 파이프라인 디코드 오류가 발생할 수 있습니다.</p> <p>・ 16097:광고 중단 중 발생한 오류는 처리되지 않으므로 기본 스트림이 재생을 중지할 수 있습니다.</p> <p>・ 18095:MP4 광고는 HLS 라이브 콘텐츠에서 지원되지 않습니다.</p> <p>19120년:HLS 콘텐츠가 있는 HLS 광고에 대한 다중 검색 때문에 스트림이 재생을 중지할 수 있습니다.</p> <p>・ 19131:버퍼링 오버레이는 프리롤 및 브레이크에서 콘텐츠로 전환하는 동안 나타날 수 있습니다.</p> <p>・ 20296:HLS Live 스트림의 경우 DVR 창에서 다시 찾은 다음 해결된 중간 롤에 대해 검색하면 재생이 지연될 수 있습니다.</p> <p>・ 20298: 중간 롤이 있는 HLS 라이브 스트림이 첫 번째 중간 롤의 순간에 정지하고 DVR 창 밖으로 이동합니다.</p> <p>・ 20317:광고 나누기에 둘 이상의 광고가 포함되어 있는 경우 HLS 라이브 스트림은 다음 광고나 광고에서 컨텐츠로 전환하는 경우 중지할 수 있습니다.</p> 
    <ul> 
     <li>HLS 라이브 스트림의 DVR 창에 있는 광고는 확인되지 않습니다.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK는 VAST adSource에 대한 VMAP 응답 내에서 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>2077년:SDK는 VAST adSource에 대한 VMAP 응답 내의 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014년:VMAP 반복 속성은 지원되지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>크리에이티브 재패키징</td> 
   <td> </td> 
   <td>21464:광고 중단의 광고 중 하나에 대해 크리에이티브한 재패키징이 실패하는 경우 광고 응답이 완전히 무시됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 20:고급 Ad Insertion 기능(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생 전용)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>광고 전용</td> 
   <td> </td> 
   <td>20056년:Ad Only 재생 시 비어 있는 기본 컨텐츠를 기반으로 하기 때문에 플레이어 기술 속성은 관련이 없습니다</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>사용자 지정 광고 정책</td> 
   <td> </td> 
   <td><p>・ 광고 행동은 MP4 광고 및 MP4 콘텐츠에서 지원되지 않습니다.</p> <p>・ 13973:사용자 지정 광고 동작 - MSE와 함께 사용할 경우 SKIP 정책이 전체 이벤트를 발생시키지 않습니다.</p> <p>・ 14939:DASH 컨텐츠에 대해 사용자 지정 광고 동작 정책을 건너뛰고 광고 중단 건너뛰는 작업이 작동하지 않습니다.</p> <p>・ 17131:광고의 첫 번째 프레임이 표시된 다음 SKIP 광고 중단 정책의 경우 컨텐츠가 다시 시작됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>컴패니언 광고/배너 광고/클릭 가능한 광고</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>참조 플레이어를 사용하는 경우 배너 광고가 표시되지 않습니다.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ 광고 행동은 VPAID 광고에 대해 지원되지 않습니다.</p> <p>・ 15032:광고 중단에서 MP4 또는 HLS 광고와 조합된 VPAID 광고는 지원되지 않습니다.</p> <p>・ 19001:Android 및 iOS에서 기본 컨텐츠 이중 오디오 트랙이 들리므로 VPAID 광고가 MP4와 함께 재생될 때 기본 컨텐츠 중 하나와 광고 중 하나가 됩니다.</p> <p>・ 20762:VPAID 광고는 사진(PIP)에서 지원되지 않습니다.</p> <p>・ 21172:VPAID 광고가 있는 HLS VOD 콘텐츠에 대해 재생 완료 이벤트가 수신되지 않습니다.</p> <p>・ 21173:HLS VOD 콘텐츠 및 포스트롤 VPAID 광고에 onAdBreakCompleteEvent가 수신되지 않습니다.</p> </td> 
   <td>플레이어는 VPAID 및 기본 컨텐츠 간을 전환하는 동안 일반 모드와 전체 화면 모드 간에 전환합니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 21:통합**

| **컨텐츠 유형** | **기능** | **Flash** | **Firefox, IE, Chrome, Android Chrome의 HTML5** | **Safari, iOS Safari의 HTML5** | **Chromecast(DASH 재생 전용)** |
|---|---|---|---|---|---|
| VOD + 라이브 | Adobe Analytics VHL 통합 |  | 19004년:UI 구성자 도구를 통해 비디오 분석 추적을 사용할 수 없습니다. |  |  |

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 문서를 참조하십시오.