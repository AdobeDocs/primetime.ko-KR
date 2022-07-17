---
title: 브라우저 TVSDK 2.4 릴리스 노트
description: 브라우저 TVSDK 2.4 릴리스 노트에서는 브라우저 TVSDK 2.4의 새로운 기능, 지원 및 지원되지 않는 기능과 알려진 문제에 대해 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# 브라우저 TVSDK 2.4 릴리스 노트 {#browser-tvsdk-release-notes}

브라우저 TVSDK 2.4 릴리스 노트에서는 브라우저 TVSDK 2.4의 새로운 기능, 지원 및 지원되지 않는 기능과 알려진 문제에 대해 설명합니다.

## 소개 {#introduction}

브라우저 TVSDK는 브라우저 기반 비디오 플레이어 애플리케이션에 고급 비디오 재생 기능, 컨텐츠 보호 및 광고를 추가할 수 있는 툴킷입니다.

Browser TVSDK 2.4는 브라우저 기반 비디오 애플리케이션을 빌드하기 위한 JavaScript API를 제공하며 다음 모드에서 재생 지원을 포함합니다.

* HTML5만
* 자동 플래시 폴백이 있는 HTML5
* 항상 Flash

이 릴리스에는 다음 정보가 포함됩니다.

・ [브라우저 TVSDK API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [브라우저 TVSDK 프로그래밍 안내서](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [1.4 DHLS용 TVSDK - 브라우저 TVSDK 2.4로 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [브라우저 TVSDK 2.4.6에서 버전 2.4.7로 변환](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ 빌드에 포함된 참조 구현.

>[!NOTE]
>
>*이 릴리스의 보안 고려 사항 전체 목록에 대해서는 보안 고려 사항 을 참조하십시오.

## 새로운 기능 및 지원되는 기능 {#what-s-new-and-supported-features}

이 Browser TVSDK 릴리스는 비디오 애플리케이션을 향상시키는 데 사용할 수 있는 새로운 기능을 제공합니다.

**2.4.12의 새로운 업데이트(빌드 204)**

다음 추가 내용은 브라우저 TVSDK 2.4.12 업데이트(빌드 204)의 일부로 사용할 수 있습니다.

* 재생이 음소거될 때 iOS에서 자동 재생을 허용하도록 AdobePSDK.MediaPlayer의 볼륨 API 구현이 변경되었습니다.

・ 새로운 API, `auditudeSettings.ignoreVPAIDAds`Auditude 서버에서 받은 VPAID 광고를 무시할 수 있도록 가 추가되었습니다. API가 Flash 폴백에서 작동하지 않습니다.

**버전 2.4.11**

다음 개선 사항 및 추가 사항은 Browser TVSDK 2.4.11 릴리스의 일부로 사용할 수 있습니다.

・ HLS 라이브 세그먼트 페일오버는 MSE 및 Flash 폴백 모드에 대해 지원됩니다.

・ 지원 `AuditudeSettings.creativeRepackagingDomain` 이제 MSE에 API도 사용할 수 있습니다. 이전에 Flash 폴백 모드에서만 지원되었습니다.

・ 릴리스에 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 자세한 내용은 *해결된 문제* 목록.

**버전 2.4.10**

다음 개선 사항 및 추가 사항은 Browser TVSDK 2.4.10 릴리스의 일부로 사용할 수 있습니다.

・ TVSDK는 로그를 활성화하거나 비활성화하는 enableLogging() 을 제공합니다. 자세한 내용은 [API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)사용.

・ Adobe Analytics을 사용할 때 TVSDK는 더 이상 기본 장을 지원하지 않습니다. 애플리케이션을 사용하여 장을 정의하고 관리합니다.

・ 릴리스에 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 목록 *문제를 참조하십시오.

**버전 2.4.9**

다음 개선 사항 및 추가 사항은 Browser TVSDK 2.4.9 릴리스의 일부로 사용할 수 있습니다.

・ 시간 불연속성이 있지만 무중단 운영 마커가 없는 HLS VOD 및 라이브 스트림이 지원됩니다.

・ ID3 v2.4.0 프레임은 HLS VOD 및 라이브 스트림용 Safari 비디오 태그에서 지원됩니다.

・ 보안 광고 로드 구현을 통해 API 구성을 기반으로 광고 서버 호출을 보안 HTTP로 업그레이드할 수 있습니다. 자세한 내용은 AdobePSDK.AdvertisingMetadata 및 AdobePSDK.ForceHttpsAdConfiguration 클래스를 참조하십시오. 이 기능은 Flash 대체 모드에서 지원되지 않습니다.

・ VAST 3.0 응답과 관련된 광고 ID 정보 및 확장 정보는 이제 TVSDK에서 애플리케이션에서 사용할 수 있으며 광고 측정에 대한 Gazar 통합을 구현하는 데 사용할 수 있습니다. 자세한 내용은 AdobePSDK.NetworkAdInfo API를 참조하십시오. Flash 대체 모드에서는 지원되지 않습니다.

・ AdobePSDK.ForceHttpsConfiguration 클래스를 더 이상 사용할 수 없습니다. 이것은

AdobePSDK.ForceHttpsAdConfiguration 클래스입니다.

・ 이제 새 API인 AdobePSDK.optimizeFlashCalls를 사용하여 Flash 폴백 모드에서 HLS 재생 경험을 개선하기 위해 호출을 최적화할 수 있습니다. 기본적으로 비활성화되어 있습니다.

**2.4.8 업데이트(빌드 6002의 새로운 기능)**

이 업데이트에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 자세한 내용은 *해결된 문제*: 목록에 추가합니다.

**버전 2.4.8**

다음 개선 사항 및 추가 사항은 Browser TVSDK 2.4.8 릴리스의 일부로 사용할 수 있습니다.

・ SDK는 이제 Chrome EME와 호환되며 Chrome v58부터 사용 가능한 모범 사례 변경 사항이 적용됩니다. 자세한 내용은 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ 이제 UI 프레임워크에서 Flash, 광고 전용 및 타겟팅 정보 워크플로우에서 HLS 액세스 DRM을 지원합니다.

・ setDRMAuthenticateData API가 UI 프레임워크에 추가됩니다. Adobe 액세스 DRM으로 보호된 스트림을 재생하려면 이 API를 호출합니다. 또는 플레이어에서 drmAuthenticateData 속성을 지정할 수 있습니다. 자세한 내용은 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)자세한 내용

**버전 2.4.7**

버전 2.4.7의 새로운 기능은 다음과 같습니다.

・ UI 프레임워크에서 UI Configurator 추가

다음 방법 중 하나로 플레이어를 구성할 수 있습니다.

・ JSON 개체 사용

・ API 사용

JSON 개체를 생성하는 데 도움이 되도록 브라우저 TVSDK에서 **UI Configurator ** 도구를 제공합니다.

이 도구에서 다양한 설정을 선택하고 **구성 테스트**를 클릭하여 설정을 확인한 다음 **구성 다운로드**를 클릭하여 설정을 다운로드할 수 있습니다. 파일을 다운로드한 후 이 파일의 내용을 JSON 개체 로 ptp.videoPlayer API에 전달할 수 있습니다.

・ UI 프레임워크에 MediaPlayerItemConfig API 추가

advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration 등 다양한 기능을 MediaPlayerItemConfig를 통해 구성할 수 있습니다. 자세한 내용은 [브라우저 TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* [설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

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

* UI 프레임워크에서 DRM 및 Analytics 워크플로우 지원

UI 프레임워크를 통해 DRM 구성 및 Analytics 추적을 활성화할 수 있습니다.

* 추가 `AdobePSDK.embedSWFinFullScreenDiv` API

이 새 API는 FlashFallback.swf 파일을 포함할 수 있는 div를 선택할 수 있도록 플레이어 앱에 유연성을 제공합니다.

* 대체됨 `getVersion`의 API `AdobePSDK.MediaPlayer` 클래스 `AdobePSDK.Version` tvsdk 버전 관련 정보에 대한 클래스입니다. 자세한 내용은 `AdobePSDK.Version` API [여기](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**버전 2.4.6**

버전 2.4.6의 새로운 기능은 다음과 같습니다.

* **지원 찾아보기**

Browserify를 사용하면 브라우저에서 node.js 스타일 모듈을 사용할 수 있습니다. 종속성을 정의하고 모든 번들을 하나의 JavaScript 파일로 검색할 수 있습니다.

* **과금**

과금의 지원을 통해 Browser TVSDK는 Primetime 고객에게 청구하기 위해 플레이어 사용 지표를 수집할 수 있습니다.

>[!NOTE]
>
>Enum PSDKErrorCode에서 더 이상 사용되지 않는 enum MediaPlayer.Events 및 더 이상 사용되지 않는 상수가 버전 2.4.6에서 제거되었습니다. 자세한 내용은 [브라우저 TVSDK 2.4.5에서 버전 2.4.6으로 변환](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**버전 2.4.5**

버전 2.4.5의 새로운 기능은 다음과 같습니다.

* **전체 이벤트 재생 및 광고**

   이제 HLS 전체 이벤트 재생(FER) 스트림이 광고 해상도 및 광고 동작을 지원합니다. 이 지원을 활성화하려면 광고 시그널링 모드를 로 설정하십시오 `MANIFEST_CUES` 생성 시 `MediaPlayerItemConfig` 개체.

* **MediaplayerView ScalePolicy 지원**

   이제 응용 프로그램 개발자는 MediaplayerView scalePolicy 속성을 사용하여 보기에 대해 다른 scalePolicy를 지정할 수 있습니다.

* **아나모픽 컨텐츠 지원**

   이제 MSE 및 Flash 재생을 사용할 때 아나모픽 컨텐츠 재생이 지원됩니다.

* **의 선택적 응용`withCredentials`**

When `withCredentials` 이 true로 설정되어 있고, `Access-Control-Allow-Origin` 헤더를 와일드카드 태그로 설정할 수 없습니다. 서버의 응답에 따라 브라우저 TVSDK는 선택적으로 `withCredentials` 속성을 사용합니다. 이 지원에 대한 자세한 내용은 [브라우저 TVSDK API 문서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**버전 2.4.4**

다음 기능은 버전 2.4.4의 새로운 기능입니다.

* **Chromecast 샘플 앱**

이 릴리스는 클라이언트측 광고 삽입으로 DASH VOD 스트림 및 DASH Widevine 스트림을 재생하는 발신자 및 수신자 앱을 지원합니다.

* **고급 페일오버 지원**

이 릴리스에는 HLS VOD 스트림에 대한 고급 페일오버 사용 사례(세그먼트 및 서버 페일오버)를 지원하는 기능이 포함되어 있습니다.

**버전 2.4.3**

버전 2.4.3의 새로운 기능은 다음과 같습니다.

* **DASH VOD용 사용자 지정 태그**

   인라인 사용자 지정 태그(이벤트)는 TimedMetadata 개체로 구독하고 받을 수 있습니다.

* **확장이 없는 스트림 재생**

   이제 확장이 없는 HLS 및 DASH 스트림이 지원됩니다. 매니페스트 파일의 경우 리소스를 로드할 때 resourceType을 지정해야 합니다. 세그먼트 및 VTT 파일의 경우 콘텐츠 유형 응답 헤더를 사용하여 콘텐츠 유형을 확인합니다.

**버전 2.4.2**

다음 기능은 버전 2.4.2의 새로운 기능입니다.

* **API 패리티**

API 패리티의 전체 목록은 다음을 참조하십시오. [1.4 DHLS용 TVSDK - 브라우저 TVSDK 2.4로 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **샘플-AES 지원**

   이 릴리스에서는 MSE 및 Flash 폴백에서 샘플-AES 암호화 컨텐츠 재생에 대한 지원이 추가되었습니다. Google Chrome에서 보안 원본으로 AES 콘텐츠를 호스팅해야 하는 요구 사항이 제거되었습니다.

* **AAC 컨테이너 지원**

   이제 .aac 확장명의 파일 재생이 지원됩니다. 오디오 전용 스트림 또는 대체 오디오일 수 있습니다.

   >[!NOTE]
   >
   >AC3 및 향상된 AC3 코덱은 아직 지원되지 않습니다.

* **토큰화된 스트림 재생**

CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 때때로 매니페스트에서 인증 토큰을 사용하고 세그먼트 요청에서 확인을 위해 인증 토큰을 사용할 수 있으며, 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다. 이제 이러한 스트림의 재생이 지원됩니다.

**버전 2.4.1**

다음 기능은 버전 2.4.1의 새로운 기능입니다.

* **UI 프레임워크**

JavaScript 기반 비디오 플레이어 애플리케이션의 UI 개발을 가속화하기 위해 고안된 이 프레임워크는 재생/일시 중지 및 볼륨과 같은 기본 컨트롤을 포함하고 스크러빙 막대 상태 및 닫힌 캡션 설정과 같은 요소를 쉽게 추가 또는 제거할 수 있는 API로 구성됩니다. 컨트롤과 관련된 동작을 지정하고 사용자 정의 컨트롤을 만들고 플레이어 UI를 스킨할 수 있습니다. 이러한 모든 작업은 DOM 구조를 직접 조작할 필요 없이 프레임워크를 통해 수행됩니다.

* **라이브 스트림에 대한 HLS 재생 개선 사항**

이 릴리스는 광고 삽입으로 인한 불연성을 지원합니다. EXT-PROGRAM-DATE-TIME 태그 뒤에 EXT-MEDIA-SEQUENCE 태그를 사용하여 원활한 재생을 위해 적응형 비트율 프로필 간에 동기화합니다.

* **VPAID 2.0 지원**

비디오 플레이어 광고 서비스 인터페이스 정의(VPAID) 버전 2.0은 사용자를 위한 풍부한 미디어 경험을 제공하며 게시자를 통해 광고를 더 잘 타겟팅하고 광고 노출 횟수를 추적하고 비디오 컨텐츠를 수익을 창출할 수 있습니다. 이 릴리스는 VOD(Video-on-demand) 컨텐츠를 위한 선형 JavaScript VPAID 광고를 지원합니다.

* **사용자 지정 HLS 태그**

미디어 스트림은 재생 목록/매니페스트 파일에서 태그 형태의 추가 메타데이터를 휴대할 수 있습니다. 브라우저 TVSDK를 사용하여 추가 태그를 지정 및 구독할 수 있으며 이러한 태그가 매니페스트에 표시될 때 알림을 받을 수 있습니다.

* **플레이어 타임라인에 표시된 광고 마커**

이 릴리스는 VOD 및 라이브 컨텐츠에 대한 플레이어 타임라인에 광고 마커를 표시할 수 있습니다. 참조 플레이어에서 이 동작을 볼 수 있습니다.

**2.4에서 지원됨**

버전 2.4에서는 다음 기능을 사용할 수 있었습니다.

* **MP3 오디오 재생**

   이 릴리스는 MSE(Media Source Extensions)가 있는 브라우저와 Safari 비디오 태그가 있는 브라우저에서 MP3 오디오 재생을 지원합니다.

* **MP4 비디오 재생**

   지원되는 기능은 다음과 같습니다.

   * 단일 스트림 재생
   * 광고 동작 및 추적을 사용하는 프리롤 및 포스트롤 MP4 광고
   * 광고 동작 및 추적을 사용하는 프리롤 및 포스트롤 HLS 광고
   * 광고 동작 및 추적을 사용하는 프리롤 및 포스트롤 DASH 광고

## 지원되는 플랫폼 {#supported-platforms}

브라우저 TVSDK에는 실행해야 하는 플랫폼 및 소프트웨어 수준에 대한 특정 요구 사항이 있습니다. 지원되는 플랫폼 및 소프트웨어 수준은 다음과 같습니다.

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

**Google Chromecast(2세대) DASH 재생에만 해당)**

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
   <td><p>MSE<sup>2개</sup></p> </td> 
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

다음은 이 릴리스에서 지원되는 및 지원되지 않는 기능 목록입니다.

* *MP3 오디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 핵심 Ad Insertion*

>[!NOTE]
>
>*아래 기능 매트릭스 테이블에서 &#39;Y&#39;는 기능이 현재 릴리스에서 지원됨을 의미합니다.*

### MP3 오디오 기능 {#mp-audio-features}

**표 1: 코어 재생{#table-core-playback}**

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP3 VOD | 일반 재생(재생, 일시 정지, 찾기) | 지원되지 않음 | Y | Y |

1 브라우저 TVSDK 비디오 태그가 스트리밍 및 DRM을 지원하지 않습니다. 코덱과 컨테이너 지원은 모든 브라우저에서 동일하지 않습니다.

2 Firefox의 기본값은 버전 41 이전의 Flash Player입니다.

### MP4 오디오 기능 {#mp-audio-features-1}

**표 2: 코어 재생**

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP4 VOD | 일반 재생(재생, 일시 정지, 찾기) | 지원되지 않음 | Y | Y |

**표 3: 코어 Ad Insertion**

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 프리롤(MP4) | 지원되지 않음 | Y | Y |
| Ad Insertion | MP4 VOD | 포스트롤(MP4) | 지원되지 않음 | Y | Y |

HLS 또는 DASH 기능 지원에 대한 자세한 내용은 아래 을 참조하십시오.

## HLS 기능 매트릭스 {#hls-feature-matrix}

다음은 브라우저 TVSDK의 HLS 기능에 대한 기능 매트릭스입니다.

* *HLS 코어 재생*
* *HLS 고급 재생 기능*
* *HLS 컨텐츠 보호 기능*
* *HLS 코어 광고 삽입 기능*
* *HLS 고급 광고 삽입 기능*
* *HLS 통합*

>[!NOTE]
>
>*아래 기능 매트릭스 테이블에서 &#39;Y&#39;는 기능이 현재 릴리스에서 지원됨을 의미합니다.*

### HLS 기능 {#hls-features}

지원되는 기능은 다음과 같습니다.

**표 4: HLS 코어 재생**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>일반 재생(재생, 일시 정지, 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD 전송</p> </td> 
   <td><p>일반 재생(재생, 일시 정지 및 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>응용 비트율</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 캡션</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>VOD만 해당</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>매니페스트 장애 조치(Failover)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>고급 페일오버</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS 및 플레이어 알림</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>제한된 QoS 지원</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>쿠키 헤더 지원</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>버퍼 제어 매개 변수 설정</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>적응형 설정</p> <p>비트율 컨트롤</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>사용자 지정 태그</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>오디오 지연 바인딩</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 리디렉션</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 5: HLS 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오프셋에서 재생</p> </td> 
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
   <td><p>매끄러운 트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3 구문 분석</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>비연속성 마커 지원</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>토큰화된 스트림</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>과금</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 6: HLS 컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + Live</p> </td> 
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

**표 7: HLS 코어 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>프리롤(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>미드롤(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
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
   <td><p>VOD 전송</p> </td> 
   <td><p>광고 해상도 및 동작</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>기본 광고 정책</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>크리에이티브 재패키징(MP4에서 HLS로)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 8: HLS 고급 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>VOD + Live</p> </td> 
   <td><p>타깃팅 매개 변수</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>사용자 지정 매개 변수</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>사용자 지정 광고 정책</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>레이지 광고 로드</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>플랫폼 제한 사항</p> </td> 
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

**표 9: HLS 통합{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>통합</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe Analytics VHL 통합</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 대시 기능 매트릭스 {#dash-feature-matrix}

다음은 브라우저 TVSDK의 DASH 기능에 대한 기능 매트릭스입니다.

・ *DASH 코어 재생 기능*

・ *DASH 고급 재생 기능*

・ *DASH 컨텐츠 보호 기능*

・ *DASH 코어 광고 삽입 기능*

・ *DASH 고급 광고 삽입 기능*

・ *DASH 통합*

>[!NOTE]
>
>아래 기능 매트릭스 테이블에서 Y는 기능이 현재 릴리스에서 지원됨을 의미합니다.

### 대시 기능 {#dash-features}

지원되는 기능은 다음과 같습니다.

**표 10: DASH 코어 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>일반 재생(재생, 일시 정지, 검색)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD 전송</p> </td> 
   <td><p>일반 재생(재생, 일시 정지 및 검색)</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>응용 비트율</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 캡션</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>페일오버</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS 및 플레이어 알림</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>쿠키 헤더 지원</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>버퍼 제어 매개 변수 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>적응형 비트율 컨트롤 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>사용자 지정 태그(EventStream)</p> </td> 
   <td><p>VOD만 해당(인라인)</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>늦게 바인딩된 오디오</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 리디렉션</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 11: DASH 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>오프셋에서 재생</p> </td> 
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
   <td><p>매끄러운 트릭 플레이</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3 구문 분석</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>여러 기간 지원</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>토큰화된 스트림</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>과금</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 12: DASH 컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>샘플-AES</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>컨텐츠 보호</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Chrome, Firefox 47 이상 및 Chromecast의 Windows</p> <p>・ Windows 8.1 및 Edge의 Internet Explorer에서 PlayReady</p> <p>・ Windows Firefox용 Primetime DRM(비디오만 해당)</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 13: DASH 코어 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>프리롤(MP4/DASH)</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>미드롤(DASH)</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>포스트롤(MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD 전송</p> </td> 
   <td><p>광고 해상도 및 동작</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>기본 광고 정책</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>크리에이티브 재패키징(MP4에서 DASH)</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 14: DASH 고급 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
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
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>사용자 지정 매개 변수</p> </td> 
   <td><p>VOD만 해당</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>사용자 지정 광고 정책</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>레이지 광고 로드</p> </td> 
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

**표 15: DASH 통합**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>카테고리</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>통합</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe Analytics VHL 통합</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 해결된 문제 {#issues-fixed}

**2.4.12 업데이트(빌드 204)에서 해결된 문제**

다음 문제가 브라우저 TVSDK 버전 2.4.12 업데이트(빌드 204)에서 해결되었습니다.

・ **21647**- TVSDK는 오디오가 음소거될 때 iOS 장치에서 자동 비디오 재생을 허용해야 합니다.

・ **21465**- DASH Live 스트림을 재생한 후 DRM 보호 DASH 스트림을 재생할 때 오류 키 시스템 액세스 거부 메시지가 수신됩니다.

・ **21442**- 사용자 제스처로 프리롤 광고가 재생된 후 iOS Web에서 컨텐츠 자동 재생을 활성화합니다.

・ **21240**- Auditude/VMAP에서 구문 분석된 VPAID 광고를 필터링하는 API를 제공했습니다.

**버전 2.4.11에서 해결된 문제**

다음 문제가 브라우저 TVSDK 버전 2.4.11에서 해결되었습니다.

**코어 재생 기능:**

・ **19192**: 이제 TVSDK에서 TextFormat:bottomInset 및 TextFormat:safeArea를 구현합니다. 이러한 개선 사항으로 인해 컨트롤 막대가 화면에 표시되면 닫힘 캡션을 다시 배치할 수 있습니다.

・ **21009**: 닫힘 캡션은 새 캡션이 나타날 때까지 지속되지 않는 검색 시 화면에 유지됩니다.

・ **21141**: 세그먼트 추가 중 경합 조건으로 인해 뒤로 찾기가 거부됩니다.

・ **21142**: 플레이어가 초기화된 상태에서 검색 가능한 재생 범위를 사용할 수 있도록 합니다. 이러한 변경 사항으로 인해 이제 위치에서 시작 세션이 지원됩니다.

・ **21363**: DASH 스트림에 대한 광고 삽입 후 608/708 닫힌 캡션이 동기화되지 않습니다.

**광고 삽입 기능:**

・ **21179**: 이제 ad.primaryAsset.adParameters 속성을 올바르게 설정하여 VOD 컨텐츠가 포함된 미드롤 관련 문제(긴 일시 중지, 블랙 프레임)가 해결됩니다.

・ **21257**: MP4가 유효한 MIME 유형이 아니고 크리에이티브 재패키징 기능이 활성화되어 있는 경우 비트율이 가장 높은 MP4 파일이 코드 변환용으로 선택됩니다.

・ **21361**: 이제 TVSDK는 추가적인 표준화 규칙을 지원하기 위해 VAST 응답의 광고 시스템 및 크리에이티브 ID를 크리에이티브 패키지 요청에서 쿼리 매개 변수로 전달합니다.

**버전 2.4.10에서 해결된 문제**

다음 문제가 브라우저 TVSDK 버전 2.4.10에서 해결되었습니다.

**코어 재생 기능:**

・ **21060**: 불연속성을 포함하는 HLS 스트림과 함께 잘못된 코덱이 throw되고 ISO BMFF 상자가 스트림 끝까지 실행됩니다.

・ **21045**: 재생 목록의 첫 번째 비디오 재생이 완료된 후 iOS에서 자동 재생이 작동하지 않습니다.

・ **20975**: 프레임 속도는 Chrome 브라우저에서 QoS 공급자가 NaN으로 반환됩니다.

・ **20823**: 데이터가 없는 세그먼트가 발생할 때 지원되지 않는 코덱이 발생했습니다.

・ **20769**: 이제 SDK는 ABR 정책을 기반으로 즉시 전환하는 대신 현재 비트 전송률로 시작합니다.

・ **20031**: IE11(Windows 8.1)의 세로 모드에서는 비디오 화면이 작아집니다. 컨텐츠 보호 기능:

・ **19316**: HLS AES-128 스트림의 경우 암호 해독이 실패한 세그먼트를 건너뜁니다.

**버전 2.4.9에서 해결된 문제**

다음 문제가 브라우저 TVSDK 버전 2.4.9에서 해결되었습니다.

**코어 재생 기능:**

・ **13407**: 재생 중에 Firefox가 &quot;ontimeupdate&quot; 이벤트를 전송하지 않으면 DASH 스트림이 중단될 수 있습니다.

・ **16380**: MSE를 통해 시작 시간이 일치하지 않는 세그먼트를 혼합한 오디오 비디오 컨텐츠 재생 중에 ABR 스위치에서 표현 간 오디오 동기화 오류가 누적되어 오류(Chromium 문제 #663686)이 발생합니다.

・ **17985**: Firefox 브라우저에서 특정 ISO-BMFF 스트림을 재생할 때 재생이 멈춥니다(Firefox 문제 #1342913). 이 오류는 Firefox v53 이후 수정되었습니다.

・ **19141**: 처리할 수 없음(약속) 참조 오류: 너비가 정의되지 않았습니다.

・ **18997, 19299**: 세그먼트 경계에서 비디오 깜박임 문제가 발생합니다. SDK가 마지막 샘플의 컴포지션 시간 오프셋을 올바르게 계산하지 않았기 때문에 이러한 문제가 발생했습니다.

・ **19780**: Firefox v53에서 HLS 컨텐츠 및 HLS 광고에 대한 재생은 시작되지 않습니다(Firefox 문제 #354653).

・ **20046**: 프로그램 날짜 시간이 시간 메타데이터 개체로 수신되면 값이 아닌 키로 수신됩니다.

・ **20047**: useDefaultResizeHandler에 Flash 폴백 시 오류가 발생합니다.

・ **20179**: Flash 폴백이 Flash Player v25.0.0.171에서 작동하지 않습니다.

・ **20293**: Firefox가 특정 HLS 스트림에 대한 버퍼링 데이터를 중지하여 지연이 발생합니다.

・ **20626**: 지속 시간이 0인 비디오 샘플을 잘못 처리하여 플레이어에서 Chrome에 미디어 디코딩 오류가 발생합니다.

・ **20078**: 브라우저 오류 &#39;QuotaExceeded&#39;에서 재생이 중단됩니다.

・ **18639**: HLS Live Stream 608 CC 텍스트 중 일부는 철자가 잘못된 것으로 표시됩니다.

・ **20028**: ClosedCaptions 크기 매개 변수가 글꼴 크기를 변경하지 않습니다.

・ **20613**: 닫힘 캡션 상자가 서로 겹쳐서 읽기 어렵게 만듭니다.

**핵심 Ad Insertion(CSAI) 기능:**

・ **20043**: 여러 광고 및 타사 리디렉션이 있는 광고 노출 및 광고 추적 호출이 누락되었습니다.

・ **20044**: 광고 재패키징을 사용할 때 광고 브레이크의 모든 광고를 성공적으로 다시 패키지해야 합니다. 그렇지 않으면 광고 브레이크가 완전히 무시됩니다.

・ **20097**: 광고 매니페스트를 사용할 수 없는 경우 20초 동안의 시간 제한을 기다리지 않고 광고 재생을 건너뛰고 기본 컨텐츠가 즉시 다시 시작됩니다.

**버전 2.4.8 업데이트(빌드 6002)에서 해결된 문제**

다음 문제가 브라우저 TVSDK 버전 2.4.8 업데이트(빌드 6002)에서 해결되었습니다.

・ **14126:** MSE 소스 버퍼의 내부 틈으로 인해 Firefox에서 재생이 중지될 수 있습니다(문제 #1316024). 재생을 재개하려면 찾기를 시도하십시오

・ **19608:** Auditude VMAP 응답에서 시간 오프셋 값을 준수하도록 수정합니다.

・ **19635:** Windows 10에서 Internet Explorer 11의 비디오 지연을 수정합니다.

・ **19761:** HLS의 ABR 문제에 대한 수정 사항.

・ **19780:** Mozilla Firefox v53에서 중단된 HLS 컨텐츠가 있는 광고 재생 수정.

・ **19877 및 19744:** 찾기 작업 후 비트율을 선택할 때 문제가 해결됩니다. 이제 찾기 시 비트율 선택은 현재 비트율과 시작 시 비트율의 낮은 값입니다.

・ **19881:** 찾기를 3~4회 수행한 후 재생 중단 및 버퍼링 오버레이가 무한 시간 동안 나타납니다.

・ **19884:** Chrome 59 Beta VMP(Verified Media Path) 요구 사항 준수 여부를 확인합니다. bTVSDK는 Chrome 59 Beta에서 Windows DRM 콘텐츠를 재생할 수 있었습니다.

・ **19916:** UI-Framework에서 DRM 재생이 손상되었습니다. 이제 메타데이터에 정책이 없는 경우에도 acquireLicense를 호출합니다.

**버전 2.4.8에서 해결된 문제**

다음 문제가 브라우저 TVSDK 2.4.8 릴리스에서 해결되었습니다.

・ **10075**: 타임라인을 따라 검색할 때 Firefox 및 Chrome에서 재생 완료 이벤트가 수신되지 않고 Firefox에서 찾기 이벤트가 수신되지 않았습니다.

・ **15775**: Windows 8.1 Internet Explorer에서 재생 완료 이벤트를 받지 못했습니다.

・ **17306**: SSAI 스트림의 경우 재생이 지원됩니다. 결합된 광고 추적은 지원되지 않습니다.

・ **19142**: 가끔 되감기로 인해 비디오 플레이어가 버퍼링 상태로 영원히 유지됩니다.

・ **19218**: 광고 마커는 UI 프레임워크를 통해 사용할 수 없습니다.

・ **19219**: 광고 전용 재생은 UI 프레임워크를 통해 작동하지 않습니다.

・ **19222**: 재생 목록에 대해 AES-128 키가 요청되고 캐시에서 후속 요청이 제공됩니다. 이전에는 각 세그먼트에 대해 요청을 받았습니다.

・ **19597**: &quot;처리할 수 없는 유형 오류: Chrome 카나리아 빌드에서 &#39;log&#39; of undefined 속성을 읽을 수 없습니다.

・ **19605**: Flash 대체 모드에 있는 경우 adRequestDomain을 사용할 수 없습니다.

・ **19608**: HLS 라이브 스트림에 VMAP 광고가 삽입되지 않았습니다. 이제 SDK는 큐 마커를 고려하며 VMAP 응답에서 시간 오프셋 값을 사용하지 않습니다.

・ **19637**: 광고 재생만 발생하면 광고 종료 시 스크립트 오류가 발생합니다.

・ **19732**: 404 오류로 인해 CRS 재생 목록 요청이 실패했습니다. 이제 브라우저 TVSDK의 1401 및 1403 요청이 업데이트되어 이를 처리합니다.

・ **19762**: 토큰 유효성에 관계없이 유효한 라이선스가 반환되었기 때문에 setAuthenticationToken 전에 호출되도록 사용된 acquireLicense입니다. 이 문제는 현재 해결되었으며 acquireLicense가 setAuthenticationToken 응답 후에만 호출됩니다.

**버전 2.4.7에서 해결된 문제**

버전 2.4.7에서 다음 문제가 해결되었습니다.

・ **8397년**: Adobe Medium 서버를 통해 생성된 HLS 라이브 스트림은 세그먼트가 키 프레임으로 시작되지 않는 경우 재생되지 않을 수 있습니다.

・ **13606**: Chrome 브라우저의 HLS 스트림에 대해 여러 검색 관련 문제가 해결되었습니다.

・ **14807**: Chrome 브라우저에서 play() 직후에 검색 또는 일시 중지가 트리거되는 경우 DOMException 오류가 발생하여 재생이 중지될 수 있습니다. 호출이 play() 요청을 중단했습니다...(Chromium 문제# 593273).

・ **19085**: MediaPlayer 매개 변수(예: 볼륨, abrControlParameters 및 Style)가 플레이어 재설정 시 기본값으로 설정되어 있지 않습니다.

**버전 2.4.6에서 해결된 문제**

버전 2.4.6에서 다음 문제가 해결되었습니다.

・ **18093**: Flash 대체 모드에서 Flash Player 버전 24를 사용하면 구독한 태그 옆에 있는 태그에 대한 TimedMetadata가 반환됩니다.

**버전 2.4.4에서 해결된 문제**

버전 2.4.4에서 다음 문제가 해결되었습니다.

・ **8711년**: MSE를 사용하면 기본적으로 608/708 캡션이 균등하게 유지됩니다.

・ **13934**: HLS 라이브 스트림을 사용하여 재생할 때에는 광고에 대한 ABR 설정을 적용할 수 없습니다.

・ **14079**: DVR 창이 낮은 HLS 라이브 스트림의 수명은 네트워크 지연 문제로 인해 재생이 늦어질 수 있으므로 실패할 수 있습니다. 재생을 재개하려면 라이브 포인트를 클릭합니다.

・ **15037**: 플레이어 UI 프레임워크와 함께 제공된 샘플이 Windows 7의 Microsoft Internet Explorer 10에서 작동하지 않습니다.

・ **15913**: HLS VOD 스트림의 경우 Chrome에서 매니페스트 응답이 304가 수정되지 않으면 스트림이 재생되지 않습니다. Chrome v55(Chromium 문제 633696) 이후 수정되었습니다.

・ **16103**: Android Chrome의 낮은 대역폭 조건에서 Uncatch TypeError로 재생이 중지될 수 있습니다. 정의되지 않은 오류의 &#39;programDateTime&#39; 속성을 읽을 수 없습니다.

・ **16265**: HLS VOD 및 라이브 스트림의 경우 중단 간 찾기가 작동하지 않습니다.

・ **16709**: PDT 및 비연속 마커를 사용하여 HLS 라이브 스트림을 다시 시작하면 플레이어가 버퍼링에 걸릴 수 있습니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

브라우저 TVSDK의 제한 사항과 알려진 문제가 아래에 언급되어 있습니다.

**표 16: 코어 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생만)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>일반 재생(재생, 일시 정지, 찾기)</td> 
   <td><p>・ HLS 이외의 미디어 형식은 지원되지 않습니다.</p> <p>8799: Flash 대체 항목은 혼합 콘텐츠를 처리하지 않으므로 컨텐츠, 광고 및 기타 URL이 혼합 컨텐츠(보안 및 비보안 컨텐츠)로 이어지지 않도록 해야 합니다.</p> <p>・ 19271: UI 프레임워크를 통한 다중 보기 재생은 Flash 대체 모드에서 지원되지 않습니다.</p> <p>・ Windows 7의 Microsoft Internet Explorer 8 및 9에서는 이러한 버전이 SDK에서 지원되지 않으므로 Flash 폴백이 작동하지 않습니다.</p> <p>・ 20262: Flash 폴백이 사용자 지정 매개 변수를 타깃팅 정보 목록에 추가합니다. 또한 Flash 및 MSE의 경우 사용자 지정 매개 변수의 우선순위 순서가 다릅니다.</p> <p>・ 20653:Creators Update를 사용하는 Win10에서는 브라우저 TVSDK Flash 폴백이 작동하지 않습니다.</p> <p>・ Flash 폴백이 Flash Player 버전 23 이상에서 작동합니다.</p> <p>・ 20087 - Chrome 59 Beta 및</p> <p>Flash 25.0.0.171</p> <p>Beta(기본값), HLS 재생이 Flash 대체 모드에서 작동하지 않습니다. 카나리아에서는 잘 작동하고 있다.</p> </td> 
   <td><p>・ 12563: 오디오 코덱이 있는 대시 스트림은 MPD에서 지원되지 않는 오디오 코덱으로 인해 Firefox에서 재생되지 않습니다. Audio Codec mp4a.40.2가 지원됩니다.</p> <p>15029: UI-Framework에서 multiView에서 비디오 간을 전환하는 동안 재생/일시 중지 단추가 그에 따라 업데이트되지 않습니다.</p> <p>・ 16034:Windows 8.1 IE에서 reset()을 호출하면 알 수 없는 MIME 유형 오류가 발생합니다. 재생을 재개하려면 미디어를 다시 로드하십시오.</p> <p>・ 18235: 광고가 있는 DASH VOD 스트림에 특정 찾기 문제가 관찰됩니다.</p> <p>・ 18727: MSE에는 오류 API가 지원되지 않습니다</p> <p>18750: SDK 및 UI 프레임워크 및 UI 프레임워크에 대한 일부 경우 리소스가 로드된 후 추가된 이벤트 리스너에 대해 IDLE 및 Initializing StatusChange 이벤트가 누락될 수 있습니다.</p> <p>・ 18889: MediaPlayer가 ERROR 상태인 경우 보기 개체가 반환되지 않습니다.</p> <p>・ 19039: AdobePSDK인 경우. MediaPlayer. seekToLocal()은 EOF보다 큰 값과 함께 사용되면 MSE의 경우 처음부터 재생이 시작됩니다.</p> <p>・ 19049: 재생 중에 비디오가 차단되면 Chrome, IE, Firefox의 Flash Player에 대해 보고된 오류 상태가 없습니다.</p> <p>・ 17205: 오디오가 계속 재생되는 동안 비디오 재생이 고정된 스트림 재생 시 몇 시간 동안 중단됩니다(Chromium 문제# 664033).</p> <p>・ 12308: composition_time_offset이 지정된 DASH 스트림에 timeStampOffset이 Chrome 브라우저에서 적용되어 음수 디코딩 시간이 발생하므로 MEDIA_ERR_ SRC_NOT_ SUPPORTED 오류(Chromium 문제 #398141)이 발생할 수 있습니다.</p> <p>・ 14126: MSE 소스 버퍼의 내부 틈으로 인해 Firefox에서 재생이 중지될 수 있습니다(문제 번호 1316024). 재생을 재개하려면 찾기를 시도하십시오.</p> <p>・ 19115: MS Edge 및 IE 11(Win 8.1 및 10)은 CORS 리디렉션에서 Origin을 null로 설정하지 않지만, 헤더가 null이 아니므로 재생 오류가 발생하므로 실패합니다.</p> <p>・ 19861:이미 재생된 미디어에 대한 소스 버퍼의 추가 동작 문제가 발생합니다. Chrome은 moov를 포함하여 추가된 조각을 거부하여 후속 디코딩 오류가 발생합니다. (Chromium 문제 #735335)</p> <p>19921: 버퍼링이 성공적으로 수행되었더라도 특정 HLS 컨텐츠에 대한 재생이 중단됩니다(Chromium 문제 #713540).</p> <p>・ 20444:IE 및 Edge에서 버퍼된 범위를 종료하려고 하면 재생이 지연될 수 있습니다.</p> <p>・ 20511: 경우에 따라 광고가 있거나 없는 HLS 스트림에 대해 찾기 거부를 확인할 수 있습니다.</p> <p>・ 20743: Windows 10 Chrome에서 HLS 라이브 스트림은 MP4 프리롤 재생 전에 몇 초 동안 재생됩니다.</p> <p>・ 21043: 메타데이터가 없어서 초기 로드 시 비디오 차원이 정확하지 않을 수 있습니다.</p> <p>・ 21115: 재생 목록의 비디오에 프리롤 광고를 사용할 수 있는 경우 재생을 시작하려면 Android 사용자 제스처가 필요합니다.</p> <p>・ HLS Live에서 타임스탬프 롤오버를 지원하지 않습니다.</p> <p>・ AAC-SSR 오디오가 지원되지 않습니다.</p> <p>오디오 코덱의 AC3 및 향상된 AC3는 지원되지 않습니다.</p> <p>・ 타임스탬프 불연속성이 있지만 비연속성 마커가 없는 스트림의 경우</p> <p>・ 점프로 인해 재생에 결함이 있고 잘못된 검색 결과가 있을 수 있습니다.</p> <p>・ 컨텐츠 지속 시간 및 재생 지속 시간이 일치하지 않을 수 있습니다.</p> <p>・ 표현 및 표현물 간의 불연속성이 다른 방식으로 일치하면 동기화 및 지연 문제가 발생할 수 있습니다.</p> <p>・ 캡션 및 WebVTT가 스트림 끝에 가깝지 않을 수 있습니다.</p> <p>・ 타임스탬프 이동 시 오디오 코덱의 변경이 지원되지 않습니다.</p> <p>・ 광고 삽입이 지원되지 않습니다.</p> <p>・ 빠른 정방향 트릭 모드로 인해 Win 8.1 IE 11에서 재생 루프가 발생할 수 있습니다(MS 문제 #12446268).</p> <p>대시:</p> <p>・ 라이브 스트림의 경우 - 동적 유형이 있는 라이브 프로필이 지원됩니다.</p> <p>・ VoD 스트림의 경우 - 정적 유형의 라이브 프로필이 지원됩니다.</p> <p>VoD 스트림의 경우 - 온디맨드 프로필은 광고 워크플로우에 대해 인증되지 않습니다.</p> </td> 
   <td><p>・ DASH Live 및 DASH Video on Demand 스트림은 지원되지 않습니다.</p> <p>・ 전체 화면 모드에서 PIP(Picture in Picture) 비디오 재생이 iOS에서 지원되지 않습니다.</p> <p>Safari(비디오 태그) 확장의 경우 올바른 컨텐츠 유형 헤더가 없는 덜 매니페스트가 작동하지 않습니다.</p> </td> 
   <td><p>・ 보낸 사람 앱의 applicationID는 받는 사람의 URL을 사용자 지정 수신자 앱으로 등록할 때 생성된 것과 같아야 합니다.</p> <p>・ 참조 플레이어가 DASH 워크플로우에 대해 인증되었습니다. UI 프레임워크가 인증되지 않았습니다.</p> <p>지원되는 미디어 코덱의 목록은 <a href="https://developers.google.com/cast/docs/media"><em>여기</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>VOD 전송</td> 
   <td>일반 재생(재생, 일시 정지, 찾기)</td> 
   <td> </td> 
   <td>18098: HLS LBA FER 스트림에서는 특정 검색 문제가 관찰됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>적응형 비트율</td> 
   <td><p>・ 20079: 버퍼링된 범위 내에서 찾기 시 버퍼를 다시 작성합니다.</p> <p>20080: Flash ABR 동작이 MSE와 일치하지 않습니다.</p> </td> 
   <td><p>・ 버퍼 관련 제한 사항으로 인해 ABR 스트림의 대체 변형이 무시됩니다.</p> <p>・ 12289: ABR 컨트롤 매개 변수는 무고정 HLS/DASH 스트림의 경우 오디오에 적용되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>608/708 캡션</td> 
   <td> </td> 
   <td><p>・ 7810: Android 4.4.4 Chrome에서는 플레이어에서 사용하는 기본 CSS 글꼴 패밀리를 지원하지 않는 것 같으므로 글꼴 스타일 변경 기능이 작동하지 않습니다.</p> <p>・ 608 캡션의 경우 CC 채널을 변경할 수 없습니다.</p> <p>・ 고급 스타일 기능은 608 캡션에서 지원되지 않습니다.</p> <p>액세서빌러티 태그를 통해 시그널링된 포함된 캡션 (608/708)이 지원됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: 플레이어에서 캡션을 표시할 때 WebVTT 파일의 영역 태그가 무시됩니다.</p> <p>・ 대시: 단편화된 /세그먼트화된 VTT 파일은 지원되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>매니페스트 장애 조치(failover)</td> 
   <td>21056: Flash 폴백이 있으면, 재생 중에 기본 스트림이 404 오류를 반환하는 경우 라이브 스트림에 대해 페일오버가 발생하지 않습니다.</td> 
   <td>매니페스트 페일오버는 컨텐츠에만 적용할 수 있으며 광고는 아닙니다.</td> 
   <td>재생 목록 장애 조치가 Safari에서 HTTP 오류 코드 404에만 작동합니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>고급 페일오버</td> 
   <td> </td> 
   <td><p>・ 세그먼트 장애 조치(failover)는 사용할 수 없는 세그먼트 건너뛰기와 계속 재생을 지원하지 않습니다.</p> <p>20533: 재생 목록의 누락된 세그먼트는 비연속성 세그먼트로 처리되어야 하며 재생은 사용 가능한 다음 세그먼트에서 재개되어야 합니다.</p> <p>21267: 페일오버로 인해 스트림 전환이 발생하면 이전 세그먼트가 다운로드될 수 있습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>QoS 및 Player 알림</td> 
   <td>21129: 폴백 Flash 경우에는 프레임 속도를 사용할 수 없습니다.</td> 
   <td><p>・ 11170:</p> <p>Flash 폴백이 있는 브라우저 TVSDK용 과 달리 MSE가 있는 브라우저 TVSDK에는 Timed_Event를 사용할 수 없습니다.</p> <p>21129: 프레임 속도는 라이브 스트림에 대해 계산되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>쿠키 헤더 지원</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials 플래그 및 쿠키 헤더는 Safari에서 지원되지 않습니다.</p> <p>21051: Safari에서 쿠키를 허용하려면 환경 설정 &gt; 개인 정보에서 "쿠키 및 웹 사이트 데이터" 설정을 활성화합니다.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>사용자 지정 태그</td> 
   <td>14763: # 이외의 사용자 지정 태그는 지원되지 않아야 합니다. 현재 폴백 Flash 중에 이러한 태그에 대한 TimedMetadata 개체가 생성되고 보고됩니다.</td> 
   <td>인밴드 사용자 지정 태그가 있는 스트림은 인증되지 않았습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>오디오 지연 바인딩</td> 
   <td> </td> 
   <td><p>・ HLS 라이브 LBA 스트림에서는 광고 삽입이 지원되지 않습니다.</p> <p>・ 17273: HLS VOD LBA 는 장애 조치 시 기본 변환으로 전환되며 마지막으로 선택한 상태로 다시 전환할 수 없습니다.</p> <p>・ 20251: HLS 라이브 LBA 스트림이 검색 시 지연될 수 있습니다.</p> <p>・ 20497: HLS LBA 무혼합 스트림에 스트림 끝에 가까운 오디오 또는 비디오 프레임이 누락된 경우 플레이어가 버퍼링 상태로 유지됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302 리디렉션</td> 
   <td> </td> 
   <td><p>15787: 302년</p> <p>XMLHttpRequest 개체의 responseURL 속성을 지원하지 않으므로 windows Edge 및 IE 브라우저에서 리디렉션 최적화가 지원되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 17: 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td>컨텐츠 유형</td> 
   <td>기능</td> 
   <td>Flash</td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생만)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>오프셋에서 재생</td> 
   <td><p>특정 오프셋 값에서 재생을 시작하는 것은 MP4 콘텐츠를 지원하지 않습니다.</p> </td> 
   <td>20492: 오프셋 값보다 앞에 오는 미드롤 광고는 컨텐츠가 오프셋 값에서 다시 시작되기 전에 재생됩니다.</td> 
   <td>오프셋 기능이 있는 재생은 iOS에서 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>트릭 플레이</td> 
   <td>부드러운 Trickplay는 iFrame 변환이 없는 스트림에 대해 작동하지 않습니다.</td> 
   <td><p>・ Trick Play 적응은 Firefox 및 Internet Explorer에서 지원되지 않으므로 이러한 브라우저에서는 역 트릭 모드를 사용할 수 없습니다.</p> <p>・ 광고와 함께 컨텐츠를 재생할 때 Trickplay를 사용할 수 없습니다.</p> <p>・ 10435: DASH 재생 중에 비디오가 Internet Explorer에서 정방향 트릭 재생 시 중지됩니다(Win 8.1)</p> <p>간헐적으로. 이러한 작업은 트릭 재생 적응 없이 비디오 요소 playbackRate 속성을 사용하기 때문에 발생합니다.</p> <p>14182: Chrome 브라우저에서 되감기 중에 검색 이벤트가 수신되지 않을 수 있으므로 트릭 모드가 작동하지 않는 경우가 있습니다.</p> <p>・ 14942: 비트릭 재생 스트림의 경우에도 Android용 Chrome에서 재생 속도를 설정할 수 있지만 설정이 적용되지 않고 재생이 일반 속도로 계속 진행됩니다.</p> <p>・ 17308: 찾기가 Trickplay 모드에서 작동하지 않습니다.</p> <p>・ 17309: Chrome 브라우저에서 역 트릭 모드는 2초 이상 유지할 수 없습니다.</p> <p>19272: DASH 스트림의 경우 Windows 10 Edge 브라우저의 버퍼링에서 트릭 재생이 복구되지 않을 수 있습니다.</p> </td> 
   <td>되감기 트릭 모드는 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>ID3 구문 분석</td> 
   <td>20346: ID3 프레임의 텍스트 인코딩 바이트 도 SDK에서 반환해야 합니다.</td> 
   <td><p>ADTS(오디오 데이터 전송 스트림)에서 사용할 수 있는 ID3 태그는 SDK에서 무시합니다.</p> <p>・ 12378: ID3 시간 메타데이터는 MSE를 지원하는 Flash 및 브라우저에서 다른 시간에 구문 분석되므로 참조 플레이어 타임라인의 표시 동작도 다릅니다.</p> <p>・ 19247: UI 프레임워크에서는 ID3 구문 분석이 지원되지 않습니다.</p> </td> 
   <td><p>・ 20323: aac 세그먼트의 첫 번째 샘플의 타임스탬프를 표시하는 데 사용되는 PRIV ID3 태그는 Safari에서 구문 분석되지 않습니다(Safari 문제 #32422733)</p> <p>・ 20350: 특정 장치(MAC OS X 10.1, iPad10 포함)에서 Safari는 트릭 모드 시 큐 변경 이벤트를 제공하지 않으므로 ID3 프레임이 수신되지 않습니다. (Safari 문제 #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>비연속성 마커 지원</td> 
   <td> </td> 
   <td><p>・ 클라이언트 측 광고 삽입은 불연속성을 포함하는 HLS 스트림에서 지원되지 않습니다.</p> <p>・ HLS 스트림의 불연속 간에 오디오 코덱을 변경할 수 없습니다.</p> <p>・ 비연속성 마커가 있는 HLS 스트림에 대해 오디오 트랙 스위치가 지원되지 않음</p> </td> 
   <td>불연속성 시퀀스 번호는 Safari에서 재생하기 위해 비연속성이 있는 HLS 스트림에 대한 요구 사항입니다.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 18: 컨텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생만)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>바이트 범위는 AES-128 암호화된 콘텐츠에서 지원되지 않습니다.</td> 
   <td>12324: IV 태그가 지정되지 않은 경우 HLS AES-128 암호화된 스트림이 Safari에서 재생되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660: HTML5 플레이어에서 만료된 PlayReady 암호화된 대시 콘텐츠에 대한 내부 서버 오류가 발생합니다.</p> <p>・ 16720: 기간 태그의 시작 속성이 누락된 경우 DASH DRM 암호화 콘텐츠가 작동하지 않습니다.</p> <p>・ 18589: Xlink를 사용하는 DRM 보호 Dash VoD 다기간 스트림에 대해서는 재생이 지원되지 않습니다.</p> <p>・ 18653: 여러 키가 있는 Windows 다중 기간 컨텐츠 재생은 첫 번째 기간에 중지되며 다음 기간으로 전환할 수 없습니다.</p> <p>・ 18656: 다른 키로 암호화된 재생 가능한 다중 기간 스트림은 재생되지 않습니다.</p> <p>Dash용 Playready 2.0이 인증되지 않았습니다.</p> <p> </p> <p> </p> </td> 
   <td>12602: Safari의 HTML5 플레이어에서 HLS Fairplay DRM 메타데이터를 반복적으로 새로 고칩니다</td> 
   <td><p>벤토4를 통해 패키지된 DASH Widevine DRM 컨텐츠를 재생할 수 있습니다. Offline Packager 및 Shaka Packager를 통해 패키지된 컨텐츠는 재생되지 않습니다. DASH PlayReady DRM이 지원되지 않습니다.</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 19: 핵심 Ad Insertion 기능(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생만)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>이전/중간/후</td> 
   <td> </td> 
   <td><p>・ HLS 라이브 컨텐츠가 있는 프리롤 광고는 이중 플레이어 모드로 재생됩니다.</p> <p>・ HLS 컨텐츠가 있는 DASH 광고 및 DASH 컨텐츠가 있는 HLS 광고는 지원되지 않습니다.</p> <p>・ 19002: MSE adBreak가 있는 HTML5 Player입니다. insertionType이 올바른 삽입 형식(예: 클라이언트 삽입 및 서버 삽입)을 나타내기 위해 올바른 값을 반환하지 않습니다.</p> <p>7794년: 기본 제어 표시줄이 전체 화면 모드로 표시되는 모바일 장치(iOS, Chrome 33 이하 또는 기본 브라우저가 있는 Android)에서 광고 재생 시 검색 창과 빠른 전달 단추를 사용할 수 있습니다.</p> <p>・ 11048: Media Source Extensions의 경우 HLS Live Content에서 ad로 전환하는 것이 매끄럽게 되지 않습니다.</p> <p>・ 16083: Android 4.4 Chrome v52에서 HLS 컨텐츠가 있는 HLS 광고가 정지된 재생 후 파이프라인 디코딩 오류가 발생할 수 있습니다.</p> <p>・ 16097: 광고 브레이크 중에 발생한 오류는 처리되지 않으므로 주 스트림이 재생을 중지할 수 있습니다.</p> <p>・ 18095: MP4 광고는 HLS 라이브 컨텐츠에서 지원되지 않습니다.</p> <p>19120: HLS 컨텐츠가 있는 HLS 광고에 대한 여러 검색 시 스트림이 재생을 중지할 수 있습니다.</p> <p>・ 19131: 버퍼링 오버레이는 프리롤 광고 브레이크에서 컨텐츠로 전환하는 동안 표시될 수 있습니다.</p> <p>・ 20296: HLS 라이브 스트림의 경우 DVR 창에서 다시 찾은 후 확인된 mid 롤에 대해 찾기를 수행하면 재생이 지연될 수 있습니다.</p> <p>・ 20298:HLS 중간 롤이 있는 라이브 스트림이 첫 번째 미드롤 광고가 DVR 창 밖으로 이동하는 순간을 지연합니다.</p> <p>・ 20317: 광고 브레이크에 둘 이상의 광고가 포함된 경우 다음 광고로 전환하거나 광고에서 컨텐츠로 전환할 때 HLS 라이브 스트림이 지연될 수 있습니다.</p> 
    <ul> 
     <li>HLS 라이브 스트림의 DVR 창에 있는 광고는 확인되지 않습니다.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK는 VAST adSource에 대한 VMAP 응답 내의 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: SDK는 VAST adSource에 대한 VMAP 응답 내의 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: VMAP 반복 속성은 지원되지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>크리에이티브 재패키징</td> 
   <td> </td> 
   <td>21464: 광고 브레이크에서 광고 중 하나에 대해 광고 재패키징이 실패하는 경우 광고 응답이 완전히 삭제됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 20: CSAI(고급 Ad Insertion 기능)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML5</strong></td> 
   <td><strong>iOS Safari의 HTML5</strong></td> 
   <td><strong>Chromecast(DASH 재생만)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>광고 전용</td> 
   <td> </td> 
   <td>20056: 광고 전용 재생의 경우 비어 있는 주 컨텐츠를 기반으로 하므로 플레이어 기술 속성은 관련이 없습니다</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>사용자 지정 광고 정책</td> 
   <td> </td> 
   <td><p>・ 광고 동작은 MP4 광고 및 MP4 콘텐츠에서 지원되지 않습니다.</p> <p>・ 13973: 사용자 지정 광고 동작 - MSE와 함께 사용할 때 SKIP 정책이 전체 이벤트를 실행하지 않습니다.</p> <p>・ 14939: 사용자 지정 광고 동작 정책이 DASH 컨텐츠에 대해 건너뛰기 및 건너뛰기 광고 브레이크가 작동하지 않습니다.</p> <p>・ 17131: 광고의 첫 프레임이 표시된 다음 SKIP 광고 브레이크 정책의 경우 컨텐츠가 다시 시작됩니다.</p> </td> 
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
   <td><p>・ 광고 동작은 VPAID 광고에 대해 지원되지 않습니다.</p> <p>・ 15032: 광고 브레이크에서 MP4 또는 HLS 광고와 함께 제공되는 VPAID 광고는 지원되지 않습니다.</p> <p>・ 19001: Android 및 iOS에서 기본 컨텐츠 이중 오디오 트랙이 들리도록 VPAID 광고가 MP4로 재생될 때 기본 컨텐츠 중 하나와 광고 중 하나가 들릴 수 있습니다.</p> <p>・ 20762: VPAID 광고는 PIP(화면 속 화면)에서 지원되지 않습니다.</p> <p>・ 21172: VPAID 광고가 있는 HLS VOD 컨텐츠에 대해 재생 완료 이벤트가 수신되지 않습니다.</p> <p>・ 21173: HLS VOD 컨텐츠 및 포스트롤 VPAID 광고에 대해 onAdBreakCompleteEvent가 수신되지 않습니다.</p> </td> 
   <td>플레이어는 VPAID 광고와 기본 컨텐츠 간을 전환하는 동안 일반 모드와 전체 화면 모드 간을 전환합니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 21: 통합**

| **컨텐츠 유형** | **기능** | **Flash** | **Firefox, IE, Chrome, Android Chrome의 HTML5** | **iOS Safari의 HTML5** | **Chromecast(DASH 재생만)** |
|---|---|---|---|---|---|
| VOD + Live | Adobe Analytics VHL 통합 |  | 19004: UI Configurator 도구를 통해 비디오 Analytics 추적을 사용할 수 없습니다. |  |  |

## 유용한 리소스 {#helpful-resources}

* 에서 전체 도움말 설명서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지.
