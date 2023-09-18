---
title: 브라우저 TVSDK 2.4 릴리스 노트
description: 브라우저 TVSDK 2.4 릴리스 노트에서는 브라우저 TVSDK 2.4의 새로운 기능, 지원되는 기능 및 지원되지 않는 기능과 알려진 문제에 대해 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# 브라우저 TVSDK 2.4 릴리스 노트 {#browser-tvsdk-release-notes}

브라우저 TVSDK 2.4 릴리스 노트에서는 브라우저 TVSDK 2.4의 새로운 기능, 지원되는 기능 및 지원되지 않는 기능과 알려진 문제에 대해 설명합니다.

## 소개 {#introduction}

브라우저 TVSDK는 브라우저 기반 비디오 플레이어 애플리케이션에 고급 비디오 재생 기능, 콘텐츠 보호 및 광고를 추가할 수 있는 툴킷입니다.

브라우저 TVSDK 2.4는 브라우저 기반 비디오 애플리케이션을 빌드하기 위한 JavaScript API를 제공하며 다음 모드에서 재생 지원을 포함합니다.

* HTML 5만
* 자동 플래시 대체 기능이 있는 HTML5
* 항상 Flash

이 릴리스에는 다음 정보가 포함됩니다.

· [브라우저 TVSDK API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [브라우저 TVSDK 프로그래밍 안내서](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [1.4 DHLS용 TVSDK-브라우저 TVSDK 2.4 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [브라우저 TVSDK 2.4.6에서 버전 2.4.7로 변환](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

· 빌드에 포함된 참조 구현

>[!NOTE]
>
>*이 릴리스의 보안 고려 사항에 대한 전체 목록은 보안 고려 사항 을 참조하십시오.

## 새로운 기능 및 지원되는 기능 {#what-s-new-and-supported-features}

이 브라우저 TVSDK 릴리스에서는 비디오 애플리케이션을 개선하는 데 사용할 수 있는 새로운 기능을 제공합니다.

**2.4.12 업데이트의 새로운 기능(빌드 204)**

다음 추가는 브라우저 TVSDK 2.4.12 업데이트(빌드 204)의 일부로 사용할 수 있습니다.

* 재생이 음소거된 경우 iOS에서 자동 재생을 허용하도록 AdobePSDK.MediaPlayer의 볼륨 API 구현이 변경되었습니다.

· 새로운 API, `auditudeSettings.ignoreVPAIDAds`Auditude 서버에서 받은 VPAID 광고를 무시할 수 있도록 가 추가되었습니다. API가 Flash 폴백에 대해 작동하지 않습니다.

**버전 2.4.11**

다음 개선 사항 및 추가 사항은 브라우저 TVSDK 2.4.11 릴리스의 일부로 사용할 수 있습니다.

· HLS 라이브 세그먼트 페일오버 기능은 MSE 및 Flash 폴백 모드에서 지원됩니다.

· 지원 대상 `AuditudeSettings.creativeRepackagingDomain` 이제 MSE에서도 API를 사용할 수 있습니다. 이전에는 Flash 대체 모드에서만 지원되었습니다.

· 릴리스에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 다음을 참조하십시오 *해결된 문제* 목록을 표시합니다.

**버전 2.4.10**

다음 개선 사항 및 추가 사항은 브라우저 TVSDK 2.4.10 릴리스의 일부로 사용할 수 있습니다.

· TVSDK는 로깅을 활성화하거나 비활성화하는 enableLogging() 을 제공합니다. 다음을 참조하십시오. [API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)사용용입니다.

· Adobe Analytics을 사용할 때 TVSDK는 더 이상 기본 챕터를 지원하지 않습니다. 응용 프로그램을 사용하여 챕터를 정의하고 관리합니다.

· 릴리스에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. *해결된 문제 *목록을 참조하십시오.

**버전 2.4.9**

다음 개선 사항 및 추가 사항은 브라우저 TVSDK 2.4.9 릴리스의 일부로 사용할 수 있습니다.

· 시간 불연속성이 있지만 불연속 마커가 없는 HLS VOD 및 라이브 스트림이 지원됩니다.

· ID3 v2.4.0 프레임은 HLS VOD 및 라이브 스트림에 대한 Safari 비디오 태그에서 지원됩니다.

· 보안 광고 로드 구현을 통해 광고 서버 호출을 API 구성을 기반으로 보안 HTTP로 업그레이드할 수 있습니다. 자세한 내용은 AdobePSDK.AdvertisingMetadata 및 AdobePSDK.ForceHttpsAdConfiguration 클래스를 참조하십시오. 이 기능은 Flash 대체 모드에서 지원되지 않습니다.

· VAST 3.0 응답과 관련된 광고 ID 정보 및 확장 정보는 이제 TVSDK에서 애플리케이션에서 사용할 수 있으며, 광고 측정을 위한 Moat 통합을 구현하는 데 사용할 수 있습니다. 자세한 내용은 AdobePSDK.NetworkAdInfo API 를 참조하십시오. Flash 대체 모드에서는 지원되지 않습니다.

· AdobePSDK.ForceHttpsConfiguration 클래스를 더 이상 사용할 수 없습니다. 다음에 의해 성공했습니다.

AdobePSDK.ForceHttpsAdConfiguration 클래스.

· 이제 새로운 API인 AdobePSDK.optimizeFlashCalls를 사용하여 호출을 최적화하여 Flash 대체 모드에서 HLS 재생 환경을 개선할 수 있습니다. 이 기능은 기본적으로 비활성화되어 있습니다.

**2.4.8 업데이트의 새로운 기능(빌드 6002)**

이 업데이트에는 중요한 고객 문제에 대한 수정 사항이 포함되어 있습니다. 다음을 참조하십시오 *해결된 문제*&#x200B;목록에 대해 설명합니다.

**버전 2.4.8**

다음 개선 사항 및 추가 사항은 브라우저 TVSDK 2.4.8 릴리스의 일부로 사용할 수 있습니다.

· SDK는 이제 Chrome EME와 호환되며 Chrome v58부터 사용 가능한 모범 사례 변경 사항이 적용됩니다. 자세한 내용은 다음을 참조하십시오. [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· 이제 UI 프레임워크는 Flash, 광고 전용 및 타겟팅 정보 워크플로우에서 HLS 액세스 DRM을 지원합니다.

· setDRMAuthenticateData API가 UI 프레임워크에 추가됩니다. Adobe 액세스 DRM으로 보호된 스트림을 재생하려면 이 API를 호출합니다. 또는 플레이어에서 drmAuthenticateData 속성을 지정할 수 있습니다. 다음을 참조하십시오 [AdobePSDK.videoBehavior](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)을 참조하십시오.

**버전 2.4.7**

다음 기능은 버전 2.4.7의 새로운 기능입니다.

· UI 프레임워크에 UI Configurator 추가

다음 방법 중 하나로 플레이어를 구성할 수 있습니다.

· JSON 개체 사용

· API 사용

JSON 개체를 생성하는 데 도움이 되도록 브라우저 TVSDK는 **UI Configurator**도구를 제공합니다.

이 도구에서는 다양한 설정을 선택하고 **구성 테스트**를 클릭하여 설정을 확인하고 **구성 다운로드**를 클릭하여 설정을 다운로드할 수 있습니다. 파일을 다운로드한 후 이 파일의 컨텐츠를 JSON 개체로 ptp.videoPlayer API에 전달할 수 있습니다.

· UI 프레임워크에 MediaPlayerItemConfig API 추가

advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration 등 다양한 기능은 MediaPlayerItemConfig를 통해 구성할 수 있습니다. 자세한 내용은 다음에서 AdobePSDK.MediaPlayerItemConfig 설명서를 참조하십시오 [브라우저 TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

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

* UI 프레임워크에서 DRM 및 Analytics 워크플로 지원

UI 프레임워크를 통해 DRM 구성 및 Analytics 추적을 활성화할 수 있습니다.

* 추가 `AdobePSDK.embedSWFinFullScreenDiv` API

이 새로운 API는 플레이어 앱에서 FlashFallback.swf 파일을 포함할 수 있는 div를 선택할 수 있는 유연성을 제공합니다.

* 대체됨 `getVersion`의 API `AdobePSDK.MediaPlayer` 클래스 `AdobePSDK.Version` TVSDK 버전 관련 정보에 대한 클래스입니다. 자세한 내용은 `AdobePSDK.Version` API [여기](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**버전 2.4.6**

다음 기능은 버전 2.4.6의 새로운 기능입니다.

* **Browserify 지원**

Browserialize를 사용하면 브라우저에서 node.js 스타일 모듈을 사용할 수 있습니다. 종속성을 정의하고 모든 번들을 하나의 JavaScript 파일로 Browserialize할 수 있습니다.

* **청구**

결제를 통해 브라우저 TVSDK는 플레이어 사용 지표를 수집하여 Primetime 고객에게 청구할 수 있습니다.

>[!NOTE]
>
>Enum PSDKErrorCode에서 더 이상 사용되지 않는 enum MediaPlayer.Events 및 더 이상 사용되지 않는 상수가 버전 2.4.6에서 제거되었습니다. 자세한 내용은 [브라우저 TVSDK 2.4.5에서 버전 2.4.6으로 변환](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**버전 2.4.5**

다음 기능은 버전 2.4.5의 새로운 기능입니다.

* **전체 이벤트 재생 및 광고**

  HLS FER(Full Event Replay) 스트림은 이제 광고 해상도 및 광고 동작을 지원합니다. 이 지원을 활성화하려면 광고 신호 모드를 다음으로 설정하십시오. `MANIFEST_CUES` 을(를) 만들 때 `MediaPlayerItemConfig` 개체.

* **MediaplayerView ScalePolicy 지원**

  이제 응용 프로그램 개발자는 MediaplayerView scalePolicy 속성을 사용하여 보기에 대해 다른 scalePolicy를 지정할 수 있습니다.

* **애너모픽 콘텐츠 지원**

  이제 MSE 및 Flash 재생을 사용할 때 애너모픽 콘텐츠 재생이 지원됩니다.

* **선택적 적용`withCredentials`**

날짜 `withCredentials` 이 true로 설정되어 있으면 `Access-Control-Allow-Origin` 헤더를 와일드카드로 설정할 수 없습니다. Browser TVSDK는 서버의 응답에 따라 `withCredentials` 특성. 이 지원에 대한 자세한 내용은 [브라우저 TVSDK API 문서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**버전 2.4.4**

다음 기능은 버전 2.4.4의 새로운 기능입니다.

* **Chromecast 샘플 앱**

이 릴리스는 클라이언트측 광고 삽입이 있는 DASH VOD 스트림 및 DASH Widevine 스트림의 재생을 보여 주는 발신자 및 수신자 앱을 지원합니다.

* **고급 페일오버 지원**

이 릴리스에는 HLS VOD 스트림에 대한 고급 페일오버 사용 사례(세그먼트 및 서버 페일오버)가 지원됩니다.

**버전 2.4.3**

다음 기능은 버전 2.4.3의 새로운 기능입니다.

* **DASH VOD에 대한 사용자 지정 태그**

  인라인 사용자 지정 태그(이벤트)는 TimedMetadata 개체로 구독하고 받을 수 있습니다.

* **확장 없이 스트림 재생**

  이제 확장이 없는 HLS 및 DASH 스트림이 지원됩니다. 매니페스트 파일의 경우 리소스를 로드할 때 resourceType을 지정해야 합니다. 세그먼트 및 VTT 파일의 경우 컨텐츠 유형 응답 헤더를 사용하여 컨텐츠 유형을 결정합니다.

**버전 2.4.2**

다음 기능은 버전 2.4.2의 새로운 기능입니다.

* **API 패리티**

API 패리티의 전체 목록은 [1.4 DHLS용 TVSDK-브라우저 TVSDK 2.4 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **샘플-AES 지원**

  이 릴리스에는 MSE 및 Flash 대체 기능에서 샘플-AES 암호화 콘텐츠 재생에 대한 지원이 추가되었습니다. Google Chrome에서 보안 원본을 통해 AES 콘텐츠를 호스팅해야 하는 요구 사항이 제거되었습니다.

* **AAC 컨테이너 지원**

  이제 확장명이 .aac인 파일 재생이 지원됩니다. 오디오 전용 스트림 또는 대체 오디오일 수 있습니다.

  >[!NOTE]
  >
  >AC3 및 향상된 AC3 코덱은 아직 지원되지 않습니다.

* **토큰화된 스트림 재생**

CDN(Content Delivery Network)을 통해 전달되는 HLS 스트림은 경우에 따라 확인을 위해 매니페스트 및 세그먼트 요청에 인증 토큰을 사용할 수 있으며 이러한 토큰은 URL 매개 변수 또는 쿠키 헤더로 제공할 수 있습니다. 이제 이러한 스트림의 재생이 지원됩니다.

**버전 2.4.1**

다음 기능은 버전 2.4.1의 새로운 기능입니다.

* **UI 프레임워크**

JavaScript 기반 비디오 플레이어 애플리케이션에 대한 UI 개발을 가속화하기 위해 설계된 이 프레임워크는 재생/일시 중지 및 볼륨과 같은 기본 컨트롤을 포함하고 스크러빙 막대 상태 및 자막 설정과 같은 요소를 쉽게 추가하거나 제거하기 위한 API로 구성됩니다. 컨트롤과 관련된 동작을 지정하고, 사용자 지정 컨트롤을 만들고, 플레이어 UI의 스킨을 지정할 수 있습니다. 이 모든 작업은 프레임워크를 통해 수행되므로 DOM 구조를 직접 조작할 필요가 없습니다.

* **라이브 스트림에 대한 HLS 재생 개선 사항**

이 릴리스는 광고 삽입으로 인한 불연속성을 지원합니다. 원활한 재생을 위해 EXT-MEDIA-SEQUENCE 태그 뒤에 오는 EXT-PROGRAM-DATE-TIME 태그를 사용하여 적응형 비트율 프로필 간에 동기화합니다.

* **VPAID 2.0 지원**

비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 버전 2.0은 사용자에게 풍부한 미디어 경험을 제공하며 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다. 이 릴리스는 VOD(video-on-demand) 콘텐츠에 대한 선형 JavaScript VPAID 광고를 지원합니다.

* **사용자 지정 HLS 태그**

미디어 스트림은 재생 목록/매니페스트 파일의 태그 형태로 추가 메타데이터를 전달할 수 있습니다. 브라우저 TVSDK를 사용하면 추가 태그를 지정하고 구독할 수 있으며 이러한 태그가 매니페스트에 나타나면 알림을 받을 수 있습니다.

* **플레이어 타임라인에 표시된 광고 마커**

이 릴리스는 플레이어 타임라인에서 VOD 및 라이브 컨텐츠 모두에 대한 광고 마커를 표시할 수 있도록 지원합니다. 이 동작은 참조 플레이어에서 볼 수 있습니다.

**2.4에서 지원됨**

버전 2.4에서는 다음 기능을 사용할 수 있습니다.

* **MP3 오디오 재생**

  이 릴리스는 MSE(Media Source Extensions) 및 Safari 비디오 태그가 있는 브라우저에서 MP3 오디오 재생을 지원합니다.

* **MP4 비디오 재생**

  지원되는 기능은 다음과 같습니다.

   * 단일 스트림 재생
   * 광고 비헤이비어 및 추적을 사용하는 프리롤 및 포스트롤 MP4 광고
   * 광고 동작 및 추적을 사용하는 프리롤 및 포스트롤 HLS 광고
   * 광고 동작 및 추적이 있는 프리롤 및 포스트롤 DASH 광고

## 지원되는 플랫폼 {#supported-platforms}

브라우저 TVSDK에는 실행해야 하는 플랫폼 및 소프트웨어 수준에 대한 특정 요구 사항이 있습니다. 지원되는 플랫폼 및 소프트웨어 수준은 다음과 같습니다.

### 데스크탑 구성 {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft 윈도우

   * Edge+

* Apple

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

   * · Chrome 33+

* APPLE IOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast(2세대, DASH 재생 전용)**

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
   <td><p>Google 크롬</p> </td> 
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

다음은 이 릴리스에서 지원되는 기능 및 지원되지 않는 기능의 목록입니다.

* *MP3 오디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 코어 재생*
* *MP4 비디오 기능 — 핵심 Ad Insertion*

>[!NOTE]
>
>*아래 기능 매트릭스 테이블에서 &#39;Y&#39;는 기능이 현재 릴리스에서 지원됨을 의미합니다.*

### MP3 오디오 기능 {#mp-audio-features}

**표 1: 코어 재생{#table-core-playback}**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP3 VOD | 일반 재생(재생, 일시 중지, 찾기) | 지원되지 않음 | Y | Y |

1 브라우저 TVSDK 비디오 태그는 스트리밍 및 DRM을 지원하지 않습니다. 코덱 및 컨테이너 지원은 모든 브라우저에서 동일하지 않습니다.

2 Firefox의 경우 기본적으로 버전 41 이하에 대해 Flash Player으로 설정됩니다.

### MP4 오디오 기능 {#mp-audio-features-1}

**표 2: 코어 재생**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | MP4 VOD | 일반 재생(재생, 일시 중지, 찾기) | 지원되지 않음 | Y | Y |

**표 3: 핵심 Ad Insertion**

| 범주 | 컨텐츠 유형 | 기능 | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 프리롤(MP4) | 지원되지 않음 | Y | Y |
| Ad Insertion | MP4 VOD | 포스트롤(MP4) | 지원되지 않음 | Y | Y |

HLS 또는 DASH 기능 지원에 대한 자세한 내용은 아래를 참조하십시오.

## HLS 기능 매트릭스 {#hls-feature-matrix}

다음은 브라우저 TVSDK의 HLS 기능에 대한 기능 매트릭스입니다.

* *HLS 코어 재생*
* *HLS 고급 재생 기능*
* *HLS 콘텐츠 보호 기능*
* *HLS 핵심 광고 삽입 기능*
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
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>일반 재생(재생, 일시 중지, 찾기)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD 재생</p> </td> 
   <td><p>일반 재생(재생, 일시 중지 및 찾기)</p> </td> 
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
   <td><p>매니페스트 장애 조치</p> </td> 
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
   <td><p>버퍼 제어 매개 변수 설정</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>적응형 설정</p> <p>비트 전송률 제어</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>사용자 정의 태그</p> </td> 
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

**표 5: HLS 고급 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
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
   <td><p>불연속 마커 지원</p> </td> 
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

**표 6: HLS 콘텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe 액세스</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>페어플레이</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 7: HLS 핵심 광고 삽입 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>미드롤(HLS)</p> </td> 
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
   <td><p>VOD 재생</p> </td> 
   <td><p>광고 해상도 및 동작</p> </td> 
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
   <td><p>크리에이티브 리패키징(MP4에서 HLS로)</p> </td> 
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
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>광고만</p> </td> 
   <td><p>지원되지 않음</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>타겟팅 매개 변수</p> </td> 
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
   <td><p>사용자 지정 광고 정책</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>플랫폼 제한</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>지연 광고 로드</p> </td> 
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

**표 9: HLS 통합{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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

· *DASH 코어 재생 기능*

· *DASH 고급 재생 기능*

· *DASH 콘텐츠 보호 기능*

· *DASH 코어 광고 삽입 기능*

· *DASH 고급 광고 삽입 기능*

· *DASH 통합*

>[!NOTE]
>
>아래 기능 매트릭스 테이블에서 Y는 기능이 현재 릴리스에서 지원됨을 의미합니다.

### DASH 기능 {#dash-features}

지원되는 기능은 다음과 같습니다.

**표 10: DASH 코어 재생 기능**

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
   <td><p>일반 재생(재생, 일시 중지, 찾기)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD 재생</p> </td> 
   <td><p>일반 재생(재생, 일시 중지 및 찾기)</p> </td> 
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
   <td><p>페일오버</p> </td> 
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
   <td><p>버퍼 제어 매개 변수 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>적응형 비트 전송률 제어 설정</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>사용자 지정 태그(EventStream)</p> </td> 
   <td><p>VOD만(인라인)</p> </td> 
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

**표 11: DASH 고급 재생 기능**

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
   <td><p>VOD + 라이브</p> </td> 
   <td><p>ID3 구문 분석</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>재생</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>여러 기간 지원</p> </td> 
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

**표 12: DASH 콘텐츠 보호 기능**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>콘텐츠 보호</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Chrome, Firefox 47 이상 및 Chromecast의 Widevine</p> <p>· Windows 8.1 및 Edge의 Internet Explorer에서 PlayReady</p> <p>· Windows Firefox용 Primetime DRM(비디오만 해당)</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 13: DASH 코어 광고 삽입 기능**

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
   <td><p>미드롤(DASH)</p> </td> 
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
   <td><p>VOD 재생</p> </td> 
   <td><p>광고 해상도 및 동작</p> </td> 
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
   <td><p>크리에이티브 리패키징(MP4에서 DASH로)</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
 </tbody> 
</table>

**표 14: DASH 고급 광고 삽입 기능**

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
   <td><p>광고만</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>타겟팅 매개 변수</p> </td> 
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
   <td><p>사용자 지정 광고 정책</p> </td> 
   <td><p>지원되지 않음</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>지연 광고 로드</p> </td> 
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
   <td><p><strong>범주</strong></p> </td> 
   <td><p><strong>컨텐츠 유형</strong></p> </td> 
   <td><p><strong>기능</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>통합</p> </td> 
   <td><p>VOD + 라이브</p> </td> 
   <td><p>Adobe Analytics VHL 통합</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 해결된 문제 {#issues-fixed}

**2.4.12 업데이트(빌드 204)에서 해결된 문제**

브라우저 TVSDK 버전 2.4.12 업데이트(빌드 204)에서 다음 문제가 수정되었습니다.

· **21647**- 오디오를 음소거할 때 TVSDK에서 iOS 장치에서 자동 비디오 재생을 허용해야 합니다.

· **21465**- DASH 라이브 스트림이 재생된 후 DRM으로 보호된 DASH 스트림을 재생할 때 오류 키 시스템 액세스 거부됨이 수신됩니다.

· **21442**- 프리롤 광고가 사용자 제스처로 재생된 후 iOS 웹에서 컨텐츠 자동 재생을 활성화합니다.

· **21240**- Auditude/VMAP에서 구문 분석된 VPAID 광고를 필터링하기 위해 제공된 API입니다.

**버전 2.4.11에서 해결된 문제**

브라우저 TVSDK 버전 2.4.11에서 다음 문제가 해결되었습니다.

**코어 재생 기능:**

· **19192**: 이제 TVSDK에서 TextFormat:bottomInset 및 TextFormat:safeArea를 구현합니다. 이러한 개선 사항으로 인해 제어 막대가 화면에 표시되면 폐쇄 캡션의 위치를 변경할 수 있습니다.

· **21009**: 닫힘 캡션은 중단 없이 찾는 경우 새 캡션이 나타날 때까지 화면에 유지됩니다.

· **21141**: 세그먼트를 추가하는 중 경합 상태로 인해 뒤로 찾기가 거부되었습니다.

· **21142**: 플레이어가 INITIALIZED 상태일 때 검색 가능한 재생 범위를 사용할 수 있도록 합니다. 이러한 변경 사항으로 인해 이제 해당 위치에서 세션 시작이 지원됩니다.

· **21363**: DASH 스트림에 대한 광고 삽입 후 608/708 폐쇄 캡션이 동기화되지 않습니다.

**광고 삽입 기능:**

· **21179**: 이제 ad.primaryAsset.adParameters 속성을 올바르게 설정하여 VOD 콘텐츠와 관련된 미드롤 문제(긴 일시 중지, 검은색 프레임)가 해결되었습니다.

· **21257**: MP4가 유효한 MIME 유형이 아니고 크리에이티브 다시 패키징 기능이 활성화된 경우 가장 높은 비트 전송률을 갖는 MP4 파일이 코드 변환에 대해 선택됩니다.

· **21361**: 이제 TVSDK가 VAST 응답의 광고 시스템 및 크리에이티브 ID를 크리에이티브 패키징 요청의 쿼리 매개 변수로 전달하여 추가 표준화 규칙을 지원합니다.

**버전 2.4.10에서 해결된 문제**

브라우저 TVSDK 버전 2.4.10에서 다음 문제가 해결되었습니다.

**코어 재생 기능:**

· **21060**: 불연속성이 포함된 HLS 스트림과 스트림 끝까지 실행된 ISO BMFF 스트림에서 잘못된 코덱 오류가 발생했습니다.

· **21045**: 재생 목록의 첫 번째 비디오 재생이 완료된 후 iOS에서 자동 재생이 작동하지 않습니다.

· **20975**: Chrome 브라우저의 QoS 공급자에 의해 프레임 속도가 NaN으로 반환됩니다.

· **20823**: 데이터가 없는 세그먼트를 만났을 때 지원되지 않는 코덱 오류가 발생합니다.

· **20769**: 이제 SDK가 ABR 정책을 기반으로 즉시 전환하는 대신 검색 시 현재 비트 전송률로 시작합니다.

· **20031**: IE11(Windows 8.1)에서 세로 모드에 있으면 비디오 화면이 작아집니다. 컨텐츠 보호 기능:

· **19316**: HLS AES-128 스트림의 경우 암호 해독에 실패한 세그먼트를 건너뜁니다.

**버전 2.4.9에서 해결된 문제**

브라우저 TVSDK 버전 2.4.9에서 다음 문제가 해결되었습니다.

**코어 재생 기능:**

· **13407**: 재생 중에 Firefox에서 &quot;ontimeupdate&quot; 이벤트 전송을 중단하면 DASH 스트림이 중단될 수 있습니다.

· **16380**: MSE를 통해 시작 시간이 일치하지 않는 세그먼트의 혼합 오디오 비디오 컨텐츠 재생 중에 표시 간의 오디오 동기화 오류가 ABR 스위치에 누적되어 최종적으로 오류가 발생합니다(Chromium 문제 #663686).

· **17985**: Firefox 브라우저에서 특정 ISO-BMFF 스트림을 재생할 때 재생이 중단됩니다(Firefox 문제 #1342913). Firefox v53부터 이 문제가 해결되었습니다.

· **19141**: 찾을 수 없음(약속) 참조오류: 너비가 정의되지 않았습니다.

· **18997, 19299**: 세그먼트 경계에서 비디오 깜박임 문제. 이 문제는 SDK가 마지막 샘플의 컴포지션 시간 오프셋을 올바르게 계산하지 않았기 때문에 발생했습니다.

· **19780**: Firefox v53에서 HLS 컨텐츠 및 HLS 광고에 대해 재생이 시작되지 않습니다(Firefox 문제 #354653).

· **20046**: 프로그램 날짜 시간이 시간 메타데이터 개체로 수신될 때 값 대신 키로 수신됩니다.

· **20047**: useDefaultResizeHandler에 Flash 대체 관련 오류가 발생합니다.

· **20179**: Flash 폴백이 Flash Player v25.0.0.171에서 작동하지 않습니다.

· **20293**: Firefox에서 특정 HLS 스트림에 대한 데이터 버퍼링을 중지하여 지연이 발생합니다.

· **20626**: 플레이어가 지속 시간이 0인 비디오 샘플을 잘못 처리하여 Chrome에서 미디어 디코딩 오류가 발생합니다.

· **20078**: 브라우저 오류 &#39;QuotaExceeded&#39;에 재생이 중단됩니다.

· **18639**: HLS 라이브 스트림 608CC에서 텍스트가 철자가 틀린 것으로 표시되는 경우가 있습니다.

· **20028**: ClosedCaptions 크기 매개 변수는 글꼴 크기를 변경하지 않습니다.

· **20613**: 폐쇄 캡션 상자가 서로 겹쳐서 읽을 수 없습니다.

**CSAI(핵심 Ad Insertion) 기능:**

· **20043**: 여러 광고 및 서드파티 리디렉션이 있는 광고 노출 및 광고 추적 호출 누락.

· **20044**: 크리에이티브 다시 패키지를 사용하는 경우 광고 브레이크의 모든 광고를 성공적으로 다시 패키징해야 합니다. 그렇지 않으면 광고 브레이크가 완전히 무시됩니다.

· **20097**: 광고 매니페스트를 사용할 수 없는 경우 광고 재생을 건너뛰고 시간 제한 20초를 기다리지 않고 기본 콘텐츠를 즉시 다시 시작합니다.

**버전 2.4.8 업데이트(빌드 6002)에서 해결된 문제**

브라우저 TVSDK 버전 2.4.8 업데이트(빌드 6002)에서 다음 문제가 수정되었습니다.

· **14126:** MSE 소스 버퍼의 내부 공백으로 인해 Firefox(문제 #1316024)에서 재생이 중단될 수 있습니다. 재생을 재개하려면 찾기 시도

· **19608:** Auditude VMAP 응답의 시간 오프셋 값을 적용하도록 수정했습니다.

· **19635:** Windows 10의 Internet Explorer 11에서 비디오 중단이 수정되었습니다.

· **19761:** HLS의 ABR 문제에 대한 수정 사항.

· **19780:** Mozilla Firefox v53에서 끊어진 HLS 콘텐츠로 광고 재생을 수정합니다.

· **19877 및 19744:** 이 문제는 검색 작업 후 비트율을 선택할 때의 불일치를 수정합니다. 이제 찾기에 대한 비트율 선택은 현재 비트율의 하위 값이며 시작 시 비트율입니다.

· **19881:** 재생이 중단되고 버퍼링하는 오버레이가 3~4회 검색 후 무한한 시간 동안 나타납니다.

· **19884:** Chrome 59 Beta VMP(Verified Media Path) 요구 사항 준수 여부를 확인합니다. bTVSDK는 Chrome 59 Beta로 Widevine DRM 콘텐츠를 재생할 수 있습니다.

· **19916:** UI 프레임워크의 DRM 재생이 손상되었습니다. 이제 메타데이터에 정책이 없어도 acquireLicense를 호출합니다.

**버전 2.4.8에서 해결된 문제**

브라우저 TVSDK 2.4.8 릴리스에서 다음 문제가 해결되었습니다.

· **10075**: 타임라인 앞에서 검색할 때 재생 완료 이벤트가 Firefox 및 Chrome에서 수신되지 않았고 검색 이벤트가 Firefox에서 수신되지 않았습니다.

· **15775**: Windows 8.1 Internet Explorer에서 재생 완료 이벤트를 받지 못했습니다.

· **17306**: SSAI 스트림의 경우 재생이 지원됩니다. 결합된 광고 추적은 지원되지 않습니다.

· **19142**: 때로는 되감기를 하면 비디오 플레이어가 버퍼링 상태를 계속 유지합니다.

· **19218**: 광고 마커는 UI 프레임워크를 통해 사용할 수 없습니다.

· **19219**: 광고 전용 재생이 UI 프레임워크를 통해 작동하지 않습니다.

· **19222**: 재생 목록에 대해 AES-128 키가 한 번 요청되고 후속 요청이 캐시에서 제공됩니다. 이전에는 각 세그먼트에 대해 요청되었습니다.

· **19597**: Chrome 카나리아 빌드에 &quot;확인할 수 없는 TypeError: 정의되지 않은 속성 &#39;log&#39;를 읽을 수 없음&quot;이 표시되었습니다.

· **19605**: Flash 대체 모드에 있는 동안 adRequestDomain을 사용할 수 없습니다.

· **19608**: VMAP 광고가 HLS 라이브 스트림에 삽입되지 않았습니다. 이제 SDK는 큐 마커를 고려하며 VMAP 응답의 시간 오프셋 값에 의존하지 않습니다.

· **19637**: 광고 재생만 재생되면 광고 끝에 스크립트 오류가 발생합니다.

· **19732**: 404 오류로 인해 CRS 재생 목록 요청이 실패했습니다. 브라우저 TVSDK의 1401 및 1403 요청이 이제 업데이트되어 이 문제를 해결했습니다.

· **19762**: getLicense가 setAuthenticationToken 전에 호출되는 데 사용되었습니다. 이로 인해 토큰 유효성과 관계없이 유효한 라이선스가 반환되었습니다. 이 문제가 이제 해결되었으며 setAuthenticationToken 응답 후에만 acquireLicense가 호출됩니다.

**버전 2.4.7에서 해결된 문제**

다음 문제가 버전 2.4.7에서 해결되었습니다.

· **8397**: 세그먼트가 키 프레임으로 시작하지 않는 경우 Adobe Media Server을 통해 생성된 HLS 라이브 스트림이 재생되지 않을 수 있습니다.

· **13606**: Chrome 브라우저의 HLS 스트림에 대한 여러 찾기 관련 문제가 해결되었습니다.

· **14807**: Chrome 브라우저에서 play() 직후 찾기 또는 일시 중지가 트리거되면 DOMException 오류로 재생이 중지될 수 있습니다. play() 요청이 호출에 의해 중단되었습니다...(Chromium issue# 593273).

· **19085**: 볼륨, abrControlParameters 및 ccStyle과 같은 MediaPlayer 매개 변수는 플레이어 재설정 시 기본값으로 설정되지 않습니다.

**버전 2.4.6에서 해결된 문제**

다음 문제는 버전 2.4.6에서 해결되었습니다.

· **18093**: Flash 폴백 모드에서 Flash Player 버전 24를 사용하면 구독한 태그 옆에 있는 태그에 대한 TimedMetadata가 반환됩니다.

**버전 2.4.4에서 해결된 문제**

버전 2.4.4에서 해결된 문제는 다음과 같습니다.

· **8711**: MSE를 사용하면 기본적으로 608/708 캡션이 양쪽 정렬된 상태로 유지됩니다.

· **13934**: HLS 라이브 스트림으로 재생할 때 광고에 대한 ABR 설정을 적용할 수 없습니다.

· **14079**: 낮은 DVR 창을 사용하는 HLS 라이브 스트림의 장수는 네트워크 지연 문제로 인해 재생이 지연될 수 있으므로 실패할 수 있습니다. 라이브 포인트를 클릭하여 재생을 재개합니다.

· **15037**: 플레이어 UI 프레임워크와 함께 제공된 샘플이 Windows 7의 Microsoft Internet Explorer 10에서 작동하지 않습니다.

· **15913**: HLS VOD 스트림의 경우, Chrome에서 매니페스트 응답이 304가 수정되지 않은 경우 스트림이 재생되지 않습니다. 이 문제는 Chrome v55(Chromium 문제 633696) 이후 해결되었습니다.

· **16103**: Android Chrome의 대역폭 조건이 낮은 경우 발견되지 않은 TypeError로 재생이 중지될 수 있음: 정의되지 않은 오류의 &#39;programDateTime&#39; 속성을 읽을 수 없음.

· **16265**: HLS VOD 및 라이브 스트림의 경우 불연속성에 대한 탐색이 작동하지 않습니다.

· **16709**: PDT 및 불연속 마커를 사용하여 HLS 라이브 스트림을 다시 시작하면 플레이어가 버퍼링에 중단될 수 있습니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

브라우저 TVSDK의 제한 사항 및 알려진 문제는 아래에 설명되어 있습니다.

**표 16: 코어 재생 기능**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML 5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML 5</strong></td> 
   <td><strong>Chromecast(DASH 재생만 해당)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>일반 재생(재생, 일시 중지, 찾기)</td> 
   <td><p>· HLS 이외의 미디어 형식은 지원되지 않습니다.</p> <p>8799: Flash 폴백은 혼합 컨텐츠를 처리하지 않으므로 컨텐츠, 광고 및 기타 URL이 혼합 컨텐츠(보안 및 비보안 컨텐츠 함께)로 연결되지 않도록 해야 합니다.</p> <p>· 19271: UI 프레임워크를 통한 멀티뷰 재생은 Flash 폴백 모드에서 지원되지 않습니다.</p> <p>· SDK에서 지원되지 않는 버전이므로 Windows 7의 Microsoft Internet Explorer 8 및 9에서 Flash 폴백이 작동하지 않습니다.</p> <p>· 20262: Flash 대체 항목은 타깃팅 정보 목록에 사용자 지정 매개 변수를 추가합니다. 또한 Flash과 MSE의 경우 사용자 정의 매개변수의 우선 순위가 다릅니다.</p> <p>· 20653:작성자 업데이트가 있는 Win10에서 브라우저 TVSDK Flash 폴백이 작동하지 않습니다.</p> <p>· Flash 폴백은 Flash Player 버전 23 이상에서 작동합니다.</p> <p>· 20087 - Chrome 59 Beta</p> <p>Flash 25.0.0.171</p> <p>Beta(기본값), HLS 재생이 Flash 대체 모드에서 작동하지 않습니다. 그것은 카나리아에서 잘 작동한다.</p> </td> 
   <td><p>· 12563: MPD의 지원되지 않는 오디오 코덱 문자열로 인해 오디오 코덱 mp4a.40.02가 있는 대시 스트림이 Firefox에서 재생되지 않습니다. 오디오 코덱 mp4a.40.2가 지원됩니다.</p> <p>15029: UI 프레임워크에서 multiView의 비디오 간을 전환하는 동안 재생/일시 중지 버튼이 그에 따라 업데이트되지 않습니다.</p> <p>· 16034:Windows 8.1 IE에서 reset()을 호출하면 알 수 없는 MIME 유형 오류가 발생합니다. 재생을 재개하려면 미디어를 다시 로드하십시오.</p> <p>· 18235: 광고가 있는 DASH vod 스트림에서 특정 검색 문제가 관찰됩니다.</p> <p>· 18727: 오류 API는 MSE에서 지원되지 않습니다.</p> <p>18750: SDK와 UI 프레임워크 모두에 대해 일부 경우에 상태 변경 이벤트가 순서가 잘못되었을 수 있으며 UI 프레임워크에서는 리소스가 로드된 후 추가된 이벤트 리스너에 대해 IDLE 및 Initializing StatusChange 이벤트가 누락될 수 있습니다.</p> <p>· 18889: MediaPlayer가 ERROR 상태인 경우 보기 개체가 반환되지 않습니다.</p> <p>· 19039: AdobePSDK인 경우. MediaPlayer. seekToLocal() 이 EOF보다 큰 값으로 사용되면 MSE의 경우 재생이 시작부터 시작됩니다.</p> <p>· 19049: 재생 중에 비디오가 차단될 때 Chrome, IE, Firefox에서 Flash Player에 대해 보고된 오류 상태가 없습니다.</p> <p>· 17205: 오디오가 계속 재생되는 동안 몇 시간 동안 믹스되지 않은 스트림 재생 시 비디오 재생이 중지됩니다(Chromium 문제 번호 664033).</p> <p>· 12308: composition_ time_offset이 지정된 DASH 스트림에 Chrome 브라우저에서 timeStampOffset이 적용되어 음수 디코딩 시간이 발생할 수 있으므로 MEDIA_ERR_ SRC_NOT_ SUPPORTED 오류(Chromium 문제 #398141).</p> <p>· 14126: MSE 소스 버퍼의 내부 공백으로 인해 Firefox(문제 번호 1316024)에서 재생이 중단될 수 있습니다. 재생을 재개하려면 를 검색해 보십시오.</p> <p>· 19115: MS Edge 및 IE 11(Win 8.1 및 10)은 CORS 리디렉션에서 Origin을 null로 설정하지 않지만 헤더가 null이 아니어서 재생 오류가 발생하므로 실패합니다.</p> <p>· 19861:이미 재생된 미디어에 대한 소스 버퍼의 추가 동작에 문제가 있습니다. Chrome은 moov를 포함하여 추가된 조각을 거부하여 후속 디코딩 오류가 발생합니다. (크롬 문제 #735335)</p> <p>19921: 버퍼링이 완료되었는데도 특정 HLS 콘텐츠에 대해 재생이 중지됨(Chromium 문제 #713540)</p> <p>· 20444:IE 및 Edge에서 버퍼된 범위의 끝을 검색하면 재생이 중지될 수 있습니다.</p> <p>· 20511: 간혹 광고가 있거나 없는 HLS 스트림에 대해 검색 거부가 관찰될 수 있습니다.</p> <p>· 20743: Windows 10 Chrome에서 HLS 라이브 스트림은 MP4 프리롤 재생 전에 몇 초 동안 재생됩니다.</p> <p>· 21043: 메타데이터 부족으로 인해 초기 로드 시 비디오 차원이 정확하지 않을 수 있습니다.</p> <p>· 21115: 재생 목록의 비디오에 프리롤 광고를 사용할 수 있는 경우 재생을 시작하려면 Android 사용자 제스처가 필요합니다.</p> <p>· HLS Live는 타임스탬프 롤오버를 지원하지 않습니다.</p> <p>· AAC-SSR 오디오가 지원되지 않습니다.</p> <p>오디오 코덱 AC3 및 고급 AC3은 지원되지 않습니다.</p> <p>· 타임스탬프 불연속이지만 불연속 마커가 없는 스트림의 경우</p> <p>· 점프로 인해 재생에 결함 및 잘못된 찾기가 있을 수 있습니다.</p> <p>· 컨텐츠 지속 시간과 재생 지속 시간이 일치하지 않을 수 있습니다.</p> <p>· 표현과 표현물의 불연속성은 다른 지혜와 일치해야 동기화와 지연 문제가 발생할 수 있습니다.</p> <p>· 캡션 및 WebVTT가 스트림 끝 근처에 표시되지 않을 수 있습니다.</p> <p>· 타임스탬프 점프 간에 오디오 코덱 변경을 지원하지 않습니다.</p> <p>· 광고 삽입이 지원되지 않습니다.</p> <p>· 빠른 전송 트릭 모드를 사용하면 Win 8.1 IE 11에서 재생 루프가 발생할 수 있습니다(MS 문제 #12446268).</p> <p>대시:</p> <p>· 라이브 스트림의 경우 - 동적 유형의 라이브 프로필이 지원됩니다.</p> <p>· VoD 스트림의 경우 - 정적 유형의 라이브 프로필이 지원됩니다.</p> <p>VoD 스트림의 경우 - 온디맨드 프로필이 광고 워크플로에 대해 인증되지 않았습니다.</p> </td> 
   <td><p>· DASH Live 및 DASH Video on Demand 스트림은 지원되지 않습니다.</p> <p>· PIP(Picture in Picture) 비디오 재생은 전체 화면 모드로 iOS에서 지원되지 않습니다.</p> <p>Safari(비디오 태그) 확장에서 올바른 콘텐츠 유형 헤더가 없으면 매니페스트를 적게 사용할 수 없습니다.</p> </td> 
   <td><p>· 보낸 사람 앱의 applicationID는 받는 사람의 URL을 사용자 지정 받는 사람 앱으로 등록할 때 생성된 ID와 동일해야 합니다.</p> <p>· 참조 플레이어가 DASH 워크플로우에 대해 인증되었습니다. UI 프레임워크가 인증되지 않았습니다.</p> <p>지원되는 미디어 코덱 목록은 을 참조하십시오. <a href="https://developers.google.com/cast/docs/media"><em>여기</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>VOD 재생</td> 
   <td>일반 재생(재생, 일시 중지, 찾기)</td> 
   <td> </td> 
   <td>18098: HLS LBA FER 스트림에서 특정 찾기 문제가 관찰됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>적응형 비트율</td> 
   <td><p>· 20079: 버퍼된 범위 내에서 찾기 시 버퍼 다시 쓰기를 수행합니다.</p> <p>20080: Flash ABR 동작이 MSE와 일치하지 않습니다.</p> </td> 
   <td><p>· 버퍼 관련 제한 사항으로 인해 ABR 스트림의 오디오 전용 폴백 변형이 무시됩니다.</p> <p>· 12289: ABR 제어 매개 변수는 혼합되지 않은 HLS/DASH 스트림의 경우 오디오에 적용되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>608/708 캡션</td> 
   <td> </td> 
   <td><p>· 7810: Android 4.4.4에서 Chrome은 플레이어에서 사용하는 기본 CSS 글꼴 모음을 지원하지 않는 것 같으므로 글꼴 스타일 변경 기능이 작동하지 않습니다.</p> <p>· 608 캡션의 경우 CC 채널을 변경할 수 없습니다.</p> <p>· 고급 스타일 기능은 608 캡션에 대해 지원되지 않습니다.</p> <p>접근성 태그를 통해 신호로 제공되는 포함된 캡션(608/708)이 지원됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206: WebVTT 파일의 영역 태그는 캡션을 표시할 때 플레이어에서 무시됩니다.</p> <p>· DASH: 단편화/세그먼트화된 VTT 파일은 지원되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>매니페스트 장애 조치</td> 
   <td>21056: Flash 폴백을 사용하면 재생 중에 기본 스트림이 404 오류를 반환하는 경우 라이브 스트림에 대한 장애 조치(Failover)가 발생하지 않습니다.</td> 
   <td>매니페스트 장애 조치(failover)는 콘텐츠에만 적용할 수 있고 광고에는 적용할 수 없습니다.</td> 
   <td>누락된 재생 목록 장애 조치(failover)는 HTTP 오류 코드 404에 대해서만 Safari에서 작동합니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>고급 페일오버</td> 
   <td> </td> 
   <td><p>· 세그먼트 장애 조치(failover)는 사용할 수 없는 세그먼트를 건너뛰고 재생을 계속할 수 없습니다.</p> <p>20533: 재생 목록에 누락된 세그먼트는 불연속으로 처리해야 하며 다음 사용 가능한 세그먼트에서 재생이 재개되어야 합니다.</p> <p>21267: 페일오버로 인한 스트림 전환으로 인해 이전 세그먼트가 다운로드될 수 있습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>QoS 및 플레이어 알림</td> 
   <td>21129: Flash 폴백의 경우 프레임 속도를 사용할 수 없습니다.</td> 
   <td><p>• 11170:</p> <p>Flash 폴백이 있는 브라우저 TVSDK와 달리 MSE가 있는 브라우저 TVSDK에는 Timed_Event를 사용할 수 없습니다.</p> <p>21129: 라이브 스트림에 대해 프레임 속도가 계산되지 않습니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>쿠키 헤더 지원</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials 플래그 및 쿠키 헤더는 Safari에서 지원되지 않습니다.</p> <p>21051: Safari에서 쿠키를 허용하려면 환경 설정 &gt; 개인 정보에서 "쿠키 및 웹 사이트 데이터" 설정을 활성화합니다.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>사용자 지정 태그</td> 
   <td>14763: #으로 시작하는 이외의 사용자 지정 태그는 지원되지 않아야 합니다. 현재 TimedMetadata 개체는 Flash 대체 중에 이러한 태그에 대해 생성되고 보고됩니다.</td> 
   <td>인밴드 사용자 지정 태그가 있는 스트림은 인증되지 않았습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>지연 바인딩 오디오</td> 
   <td> </td> 
   <td><p>· 광고 삽입은 HLS 라이브 LBA 스트림에서 지원되지 않습니다.</p> <p>· 17273: 장애 조치(failover) 시 HLS VOD LBA 스트림이 기본 렌디션으로 전환되며 마지막으로 선택한 상태로 다시 전환할 수 없습니다.</p> <p>· 20251: HLS 라이브 LBA 스트림이 찾기를 중단할 수 있습니다.</p> <p>· 20497: HLS LBA 언머싱된 스트림에 스트림 끝에 누락된 오디오 또는 비디오 프레임이 있는 경우 플레이어가 버퍼링 상태를 유지합니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>302 리디렉션</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>windows Edge 및 IE 브라우저에서는 XMLHttpRequest 개체의 responseURL 속성을 지원하지 않으므로 리디렉션 최적화가 지원되지 않습니다.</p> </td> 
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
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML 5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML 5</strong></td> 
   <td><strong>Chromecast(DASH 재생만 해당)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>오프셋에서 재생</td> 
   <td><p>MP4 컨텐츠에서는 특정 오프셋 값에서 재생을 시작할 수 없습니다.</p> </td> 
   <td>20492: 오프셋 앞에 있는 미드롤 광고는 오프셋 값에서 콘텐츠가 다시 시작되기 전에 재생됩니다.</td> 
   <td>오프셋 기능이 있는 재생은 iOS에서 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>트릭 플레이</td> 
   <td>iFrame 렌디션이 없는 스트림에는 부드러운 트리크플레이가 작동하지 않습니다.</td> 
   <td><p>· Firefox 및 Internet Explorer에서는 트릭 플레이 조정이 지원되지 않으므로 이러한 브라우저에서는 역방향 트릭 모드를 사용할 수 없습니다.</p> <p>· 광고와 함께 콘텐츠를 재생할 때는 trickplay를 사용할 수 없습니다.</p> <p>· 10435: DASH 재생 중에 Internet Explorer에서 앞으로 트릭 재생(Win 8.1)에서 비디오가 멈춥니다.</p> <p>간헐적으로 이 문제는 trick play에 적응하지 않고 비디오 요소 playbackRate 속성을 사용하기 때문에 발생합니다.</p> <p>14182: 때때로 Chrome 브라우저에서 되감는 동안 찾기 이벤트가 수신되지 않을 수 있으므로 트릭 모드가 작동하지 않습니다.</p> <p>· 14942: 비트릭 재생 스트림의 경우에도 Android용 Chrome에서 재생 속도를 설정할 수 있지만 설정이 적용되지 않고 재생이 일반 속도로 계속됩니다.</p> <p>· 17308: 찾기가 trickplay 모드에서 작동하지 않습니다.</p> <p>· 17309: Chrome 브라우저에서는 역방향 트릭 모드를 2초 이상 유지할 수 없습니다.</p> <p>19272: DASH 스트림의 경우 Windows 10 Edge 브라우저에서 버퍼링이 복구되지 않을 수 있습니다.</p> </td> 
   <td>되감기 트릭 모드는 지원되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>ID3 구문 분석</td> 
   <td>20346: ID3 프레임의 텍스트 인코딩 바이트도 SDK에서 반환해야 합니다.</td> 
   <td><p>ADTS(오디오 데이터 전송 스트림)에서 사용할 수 있는 ID3 태그는 SDK에서 무시됩니다.</p> <p>· 12378: MSE를 지원하는 Flash 및 브라우저에서 ID3 시간 메타데이터가 다른 시간에 구문 분석되므로 참조 플레이어 타임라인의 표시 동작도 다릅니다.</p> <p>· 19247: ID3 구문 분석은 UI 프레임워크에서 지원되지 않습니다.</p> </td> 
   <td><p>· 20323: aac 세그먼트의 첫 번째 샘플의 타임스탬프를 시그널링하는 데 사용되는 PRIV ID3 태그가 Safari에 의해 구문 분석되지 않습니다(Safari 문제 #32422733)</p> <p>· 20350: 특정 장치(MAC OS X 10.1, iPad10 포함)에서 Safari는 트릭 모드에 있을 때 큐 변경 이벤트를 제공하지 않으므로 ID3 프레임이 수신되지 않습니다. (Safari 문제 #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>불연속 마커 지원</td> 
   <td> </td> 
   <td><p>· 클라이언트측 광고 삽입은 불연속성이 포함된 HLS 스트림에서 지원되지 않습니다.</p> <p>· HLS 스트림의 불연속 전체에서 오디오 코덱을 변경할 수 없습니다.</p> <p>· 불연속 마커가 있는 HLS 스트림에 대해서는 오디오 트랙 스위치가 지원되지 않습니다.</p> </td> 
   <td>불연속 시퀀스 번호는 Safari에서 재생하기 위해 불연속성이 있는 HLS 스트림의 요구 사항입니다.</td> 
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
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML 5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML 5</strong></td> 
   <td><strong>Chromecast(DASH 재생만 해당)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>바이트 범위는 AES-128 암호화 콘텐츠에서 지원되지 않습니다.</td> 
   <td>12324: IV 태그가 지정되지 않은 경우 HLS AES-128 암호화된 스트림이 Safari에서 재생되지 않습니다.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660: HTML5 플레이어에서 만료된 PlayReady 암호화된 대시 콘텐츠에 대해 내부 서버 오류가 발생합니다.</p> <p>· 16720: period 태그의 start 속성이 누락된 경우 DASH DRM 암호화 콘텐츠가 작동하지 않습니다.</p> <p>· 18589: Xlink를 사용하는 DRM 보호 대시 VoD 다기간 스트림에 대해서는 재생이 지원되지 않습니다.</p> <p>· 18653: 여러 키가 있는 Widevine MultiPeriod 콘텐츠 재생이 첫 번째 기간에서 중지되고 다음 기간으로 전환할 수 없습니다.</p> <p>· 18656: 다른 키로 암호화된 Playready MultiPeriod 스트림이 재생되지 않습니다.</p> <p>Dash용 Playready 2.0이 인증되지 않았습니다.</p> <p> </p> <p> </p> </td> 
   <td>12602: HLS 페어플레이 DRM 메타데이터는 Safari의 HTML 5 플레이어에 의해 반복적으로 새로 고쳐집니다.</td> 
   <td><p>벤투4를 통해 패키지화된 DASH 와이드바인 DRM 콘텐츠가 재생될 수 있다. Offline Packager 및 Shaka packager를 통해 패키징된 콘텐츠는 재생되지 않습니다. DASH PlayReady DRM은 지원되지 않습니다.</p> </td> 
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
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML 5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML 5</strong></td> 
   <td><strong>Chromecast(DASH 재생만 해당)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>이전/중간/이후</td> 
   <td> </td> 
   <td><p>· HLS 라이브 콘텐츠가 있는 프리롤 광고는 듀얼 플레이어 모드에서 재생됩니다.</p> <p>· HLS 콘텐츠가 포함된 DASH 광고와 DASH 콘텐츠가 포함된 HLS 광고는 지원되지 않습니다.</p> <p>· 19002: MSE adBreak가 있는 HTML5 플레이어에서 insertionType은 올바른 삽입 유형(예: 클라이언트 삽입 및 서버 삽입)을 나타내기 위해 올바른 값을 반환하지 않습니다.</p> <p>7794: 모바일 장치(iOS, Chrome 33 이하 또는 기본 브라우저를 사용하는 Android)에서 기본 컨트롤 막대가 전체 화면 모드로 표시되면 광고 재생 시 이동 막대 및 빨리 감기 버튼을 사용할 수 있습니다.</p> <p>· 11048: 미디어 소스 확장의 경우 광고에서 HLS 라이브 컨텐츠로 전환이 원활하지 않습니다.</p> <p>· 16083: Android 4.4 Chrome v52에서 때때로 HLS 콘텐츠가 포함된 HLS 광고로 인해 재생이 중단된 후 파이프라인 디코딩 오류가 발생할 수 있습니다.</p> <p>· 16097: 광고 브레이크 중에 발생한 오류가 처리되지 않아 기본 스트림이 재생을 중지할 수 있습니다.</p> <p>· 18095: MP4 광고는 HLS 라이브 콘텐츠에서 지원되지 않습니다.</p> <p>19120: HLS 콘텐츠가 있는 HLS 광고에 대한 여러 찾기로 인해 스트림이 재생을 중지할 수 있습니다.</p> <p>· 19131: 프리롤 광고 브레이크에서 컨텐츠로 전환하는 동안 버퍼링 오버레이가 나타날 수 있습니다.</p> <p>· 20296: HLS 라이브 스트림의 경우 DVR 창에서 다시 검색한 다음 해결된 중간 롤을 검색하면 재생이 중단될 수 있습니다.</p> <p>· 20298:중간 롤이 있는 HLS 라이브 스트림은 첫 번째 중간 롤과 DVR 창 밖으로 이동하는 순간을 지연시킵니다.</p> <p>· 20317: 광고 브레이크에 둘 이상의 광고가 포함된 경우 다음 광고로 전환하거나 광고에서 콘텐츠로 전환할 때 HLS 라이브 스트림이 중단될 수 있습니다.</p> 
    <ul> 
     <li>HLS 라이브 스트림의 DVR 창에 있는 광고가 확인되지 않습니다.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK는 VAST adSource에 대한 VMAP 응답 내의 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: SDK는 VAST adSource에 대한 VMAP 응답 내의 시퀀스 속성을 준수하지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: VMAP 반복 속성은 지원되지 않습니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>크리에이티브 리패키징</td> 
   <td> </td> 
   <td>21464: 광고 브레이크에 있는 광고 중 하나에 대해 크리에이티브 다시 패키징에 실패하면 광고 응답이 완전히 삭제됩니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 20: 고급 Ad Insertion 기능(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>기능</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox, IE, Chrome, Android Chrome의 HTML 5</strong></td> 
   <td><strong>Safari, iOS Safari의 HTML 5</strong></td> 
   <td><strong>Chromecast(DASH 재생만 해당)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>광고만</td> 
   <td> </td> 
   <td>20056: 플레이어 기술 속성은 광고 전용 재생의 경우 비어 있는 기본 콘텐츠를 기반으로 하므로 관련이 없습니다</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + 라이브</td> 
   <td>사용자 지정 광고 정책</td> 
   <td> </td> 
   <td><p>· MP4 광고 및 MP4 콘텐츠에서는 광고 행동이 지원되지 않습니다.</p> <p>· 13973: 사용자 지정 광고 동작 - MSE와 함께 사용할 때 SKIP 정책이 완료 이벤트를 발생시키지 않습니다.</p> <p>· 14939: 사용자 지정 광고 동작 정책 건너뛰기 및 건너뛰기 광고 브레이크가 DASH 콘텐츠에 대해 작동하지 않습니다.</p> <p>· 17131: 광고의 첫 번째 프레임이 표시되면 광고 건너뛰기 정책의 경우 컨텐츠가 다시 시작됩니다.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>컴패니언 광고/ 배너 광고/ 클릭 가능한 광고</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>참조 플레이어를 사용할 때 배너 광고가 표시되지 않습니다.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID 광고에 대해서는 광고 행동이 지원되지 않습니다.</p> <p>· 15032: 광고 브레이크에서 MP4 또는 HLS 광고와 함께 VPAID 광고를 지원하지 않습니다.</p> <p>· 19001: Android 및 iOS에서 VPAID 광고가 MP4를 기본 콘텐츠로 재생될 때 더블 오디오 트랙이 들리고, 기본 콘텐츠 중 하나와 광고 중 하나입니다.</p> <p>· 20762: VPAID 광고는 PIP(Picture in Picture)에서 지원되지 않습니다.</p> <p>· 21172: VPAID 광고가 있는 HLS VOD 컨텐츠에 대해 재생 완료 이벤트가 수신되지 않습니다.</p> <p>· 21173: onAdBreakCompleteEvent가 HLS VOD 콘텐츠 및 게시물 롤 VPAID 광고에 대해 수신되지 않습니다.</p> </td> 
   <td>플레이어가 VPAID 광고와 기본 컨텐츠 간을 전환하는 동안 일반 모드와 전체 화면 모드 간을 전환합니다.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**표 21: 통합**

| **컨텐츠 유형** | **기능** | **Flash** | **Firefox, IE, Chrome, Android Chrome의 HTML 5** | **Safari, iOS Safari의 HTML 5** | **Chromecast(DASH 재생만 해당)** |
|---|---|---|---|---|---|
| VOD + 라이브 | Adobe Analytics VHL 통합 |  | 19004: UI Configurator 도구를 통해 Video Analytics 추적을 사용할 수 없습니다. |  |  |

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
