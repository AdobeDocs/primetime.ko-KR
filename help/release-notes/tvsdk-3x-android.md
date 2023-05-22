---
title: Android용 TVSDK 3.15 릴리스 노트
description: Android용 TVSDK 3.15 릴리스 노트에서는 TVSDK Android 3.15의 새로운 기능 또는 변경 사항, 해결된 문제 및 알려진 문제, 장치 문제를 설명합니다
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Android용 TVSDK 3.15 릴리스 노트 {#tvsdk-for-android-release-notes}

TVSDK Android 3.15용 TVSDK 릴리스 노트에서는 TVSDK Android 3.15의 새로운 기능 또는 변경 사항, 해결된 문제 및 알려진 문제, 장치 문제에 대해 설명합니다.

Android 참조 플레이어는 배포의 샘플/디렉터리에 있는 Android TVSDK에 포함되어 있습니다. 함께 제공되는 README.md 파일에는 참조 플레이어를 빌드하는 방법이 설명되어 있습니다.

>[!NOTE]
>
>릴리스와 함께 배포된 README.md에 설명된 대로 참조 플레이어를 성공적으로 빌드하려면 다음을 수행하십시오.
>
>1. 에서 VideoHeartbeat.jar 다운로드 [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Android v2.0.0용 VideoHeartbeat 라이브러리)
>1. VideoHeartbeat.jar를 libs/ 폴더에 추출합니다.


Android용 TVSDK는 이전 버전에 비해 많은 성능 향상을 제공합니다. 고품질 시청 환경을 제공하며 Multi-CDN 지원을 제외하고 버전 1.4의 모든 기능을 제공합니다.

지원되는 기능과 지원되지 않는 기능의 포괄적인 집합은 [기능 매트릭스](#feature-matrix) 릴리스 정보 섹션에 자세히 설명되어 있습니다.

## Android TVSDK 3.15

이 버전에서는 creative 태그가 없거나 다음과 같은 경우 애플리케이션이 여러 번 충돌하는 문제를 해결했습니다 [!UICONTROL url CDATA] 다음에서 비어 있음: [!UICONTROL VAST] 응답.

이 버전 및 이전 버전의 버그 수정에 대한 자세한 내용은 [android용 TVSDK에서 해결된 문제](#resolved-issueszd).

### 이전 릴리스의 새로운 기능 및 향상된 기능

**Android TVSDK 3.14**

이 버전에서는 다음과 같은 경우 애플리케이션이 충돌하는 문제를 해결합니다. [!UICONTROL CDATA] 노드가 다음 중 하나에 대해 비어 있음: [!UICONTROL ClickTracking], [!UICONTROL CustomClick] 또는 [!UICONTROL CompanionClickTracking] 요소를 VAST 응답에 추가합니다.

**Android TVSDK 3.13**

Fire TV 3세대 펜던트와 Fire TV Cube 1세대 및 2세대 장치가 포함된 FireTV 장치의 ABR 스위치에서 Widevine DRM 스트림이 정지하거나 검은색 프레임을 표시합니다.

문제를 해결하려면 API를 설정합니다 `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` 재생을 시작하기 전에 지정된 Fire TV 장치에 대해 설명합니다. 기본값은 false입니다.

**Android TVSDK 3.12**

Primetime 참조 애플리케이션의 gradle 버전이 버전 5.6.4로 업데이트되었습니다.

Android Studio를 사용하여 참조 앱을 설정하고 실행하려면 TVSDK zip에서 사용할 수 있는 ReadMe 파일의 지침을 따르십시오. `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

현재 릴리스에서 해결된 주요 고객 문제는에서 설명합니다. [해결된 문제](#resolved-issues) 섹션.

**Android TVSDK 3.11**

* **PSSH(보호 시스템 특정 헤더) 상자 가져오기 허용** - TVSDK를 사용하면 현재 로드된 미디어 리소스와 연결된 보호 시스템 특정 헤더 상자를 가져올 수 있습니다. 새 API `getPSSH()` 이(가)에 추가됨 `com.adobe.mediacore.drm.DRMManager`.

자세한 내용은 [와이드빈](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

이 릴리스는에서 언급했듯이 주요 고객 문제를 해결하는 데 중점을 둡니다 [해결된 문제](#resolved-issues) 섹션.

**Android TVSDK 3.9**

* **HTTPS를 통한 보안 게재** - Android TVSDK 3.9에서는 HTTPS를 통한 보안 전달 기능을 도입하여 탁월한 규모와 성능으로 콘텐츠를 안전하게 전달할 수 있었습니다.

   HTTPS를 통한 보안 전달을 활성화하려면에 새로운 API가 도입되었습니다. `NetworkConfiguration` 클래스.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **부분 광고 브레이크 기능을 사용한 프리롤 지원** - 이 향상된 기능을 통해 TVSDK 3.8은 PABI(부분 광고 브레이크 기능)가 포함된 프리롤 광고를 지원합니다.

프리롤 광고(사용 가능한 경우)가 재생되면 라이브 TV 환경을 에뮬레이션하여 라이브 포인트에서 콘텐츠가 재생됩니다.

**Android TVSDK 3.7**

* Widevine 테스트 컨텐츠의 경우 새 API `setMediaDrmCallback` DRMManager 클래스에서 MediaDrmCallback 인터페이스의 기본 구현을 재정의하기 위해 노출됩니다.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 처리하지 않음에 대한 AppCrash 오류를 수정했습니다. `MediaPlayerEvent.ITEM_UPDATED` C++ 레이어(Android 64비트)에서

**Android TVSDK 3.6**

* **64비트 요구 사항에 맞게 앱 개선** - 기본 라이브러리 `(libAVEAndroid.so)` 는 현재 업그레이드되어 두 버전에서 사용할 수 있습니다. 기존 armeabi(32비트) 기본 라이브러리 위치가에서 변경되었습니다. `/framework/Player to /framework/Player/armeabi` 그리고 추가 arm64-v8a(64비트) 라이브러리가 `/framework/Player/arm64-v8a.`

**버전 3.5**

* **적시 광고 해상도** - TVSDK 3.5는 타임라인에서 재생된 광고에 대한 지원을 제거합니다.

* **오프라인 재생 지원이 활성화되었습니다.** - 오프라인 재생을 사용하면 사용자는 이제 비디오 콘텐츠를 장치에 다운로드하고 연결되지 않은 상태에서 시청할 수 있습니다. 자세한 내용은 &quot;[Android에서 오프라인 재생](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**버전 3.4**

* TVSDK는 이제 CBC 암호화 및 일반 스트림에 대한 CMAF 스트림 재생을 지원합니다.

**버전 3.3**

* **API 변경 사항**

   * 새 API가에 추가됩니다. `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` 네트워크 오류 및 시간 초과를 처리합니다.
      * 여기서 (n)은 재시도 횟수입니다.

**버전 3.2**

* **병렬 광고 해결 및 매니페스트 다운로드 지원**

   * TVSDK 3.2는 VMAP을 제외한 모든 광고 요청 및 광고 브레이크에 대한 순차적 해결 대신 동시 해결을 지원합니다.

   * 광고 브레이크에 있는 모든 광고 매니페스트가 동시에 다운로드됩니다.

* **광고 확인 및 매니페스트 다운로드 시간 초과에 대한 지원이 활성화되었습니다.**

   * 이제 사용자는 전체 광고 해상도 및 매니페스트 다운로드에 대해 시간 초과 값을 설정할 수 있습니다.  VMAP의 경우, 모든 광고 브레이크가 순차적으로 해결되므로 개별 광고 브레이크에 시간 초과 값이 적용됩니다.

* **AdvertisingMetadata 클래스에 새로운 API가 도입되었습니다.**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **AdvertisingMetadata 클래스에서 아래 API가 제거됨:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **AC3/EAC3 오디오 코덱을 사용하여 스트림 재생 활성화**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 위치: `MediaPlayer` 클래스

* **TVSDK는 암호화된 Widevine CTR에 대해 CMAF 및 일반 스트림 재생을 지원합니다.**

* **이제 4K HEVC 스트림들의 재생이 지원된다.**

* **병렬 광고 호출 요청** - 이제 TVSDK가 20개의 광고 호출 요청을 동시에 프리페치합니다.

**버전 3.0**

* **TVSDK 3.0은 HEVC(High Efficiency Video Coding) 스트림을 지원합니다.**

* **적시 - 광고 마커에 더 가까운 광고 해결**
이제 지연 광고 해결은 각 광고 브레이크를 독립적으로 해결합니다. 이전에는 광고 해결이 2단계 접근 방식이었습니다. 사전 롤은 재생 시작 전에 해결되었고 모든 중간/사후 롤 슬롯은 재생이 시작된 후에 결합되었습니다. 이 향상된 기능을 통해 이제 각 광고 브레이크가 광고 큐 포인트 이전의 특정 시간에 해결됩니다.

>[!NOTE]
>
>레이지 광고 해결 기능이 이제 기본적으로 꺼져 있으므로 명시적으로 활성화해야 합니다.

새 API가에 추가됩니다. `AdvertisingMetadata::setDelayAdLoadingTolerance` 이 광고 메타데이터와 연결된 지연된 광고 로드 허용 한도를 가져옵니다.\
이제 준비 후 즉시 찾기가 허용되며, 광고 브레이크에 대한 찾기는 찾기를 완료하기 전에 즉시 해결됩니다.\
신호 처리 모드 `SERVER_MAP` 및 `MANIFEST_CUES` 이 지원됩니다.

자세한 내용은 [Android 프로그래머용 TVSDK 3.0 안내서](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) API 및 이벤트 변경 사항에 대해 설명합니다.

* **업데이트됨 `targetSdkVersion` 최신 버전으로**

업데이트됨 `targetSdkVersion` 원활한 작동을 위해 19세에서 27세까지.

* **Placement.Type getPlacementType()은 이제 TimelineMarker 인터페이스의 메서드입니다.**

   이 메서드는 Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL 또는 Placement.Type.Placement_ROLL의 POST 유형을 반환합니다. 광고 브레이크가 해결되지 않으면 TimelineMarker 인터페이스의 getDuration() 메서드가 0을 반환합니다.

**버전 2.5.6.**

* **TVSDK 2.5는 Android P를 지원합니다.**

* **배경 오디오 활성화**

   앱이 전경에서 배경으로 이동할 때 오디오 재생을 활성화하려면 앱이 `enableAudioPlaybackInBackground` 플레이어가 PREPARED 상태에 있을 때 인수가 true인 MediaPlayer의 API입니다.

* **MediaPlayer 클래스의 alwaysUseAudioOutputLatency(boolean val)**

설정된 경우 오디오 타임스탬프 계산에서 출력 지연 을 사용합니다.
부울 매개 변수 val - True로 설정하면 오디오 타임스탬프 계산에서 오디오 출력 지연 시간이 사용됩니다.

* **대역폭 속도가 갑자기 떨어지는 경우에도 최상의 재생 환경을 제공하도록 최적화되었습니다.**

이제 TVSDK는 필요한 경우 진행 중인 세그먼트의 다운로드를 취소하고 적절한 렌디션으로 동적으로 전환합니다. 이는 중단 없이 비트율 사이를 원활하게 전환함으로써 이루어진다.

**버전 2.5.5**

* **부분 광고 브레이크 삽입**

   부분적으로 시청한 광고에 대한 추적을 실행하지 않고 광고 중간에 참여하는 TV와 같은 경험.\
   예: 사용자가 3개의 30초 광고로 구성된 90초 광고 브레이크 중간(40초)에 참가합니다. 중간 광고 두 번째 광고에 10초입니다.

   * 두 번째 광고가 나머지 기간(20초) 동안 재생되고 세 번째 광고가 재생됩니다.

   * 재생되는 부분 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고의 추적기만이 발사된다.

* **HTTPS를 통한 보안 광고 로드**

   Adobe Primetime은 https를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

* **AdSystem 및 Creative Id가 CRS 요청에 추가됨**

   이제 포함 `AdSystem` 및 `CreativeId` (1401 및 1403 요청의 새 매개 변수).

* **NetworkConfiguration 클래스에서 API setEncodeUrlForTracking이 제거됨** 를 사용해야 하므로 URL의 안전하지 않은 문자를 인코딩해야 합니다.

**버전 2.5.4**

Android TVSDK v2.5.4는 다음 업데이트 및 API 변경 사항을 제공합니다.

* 의 기본값 변경 `WebViewDebbuging`

   `WebViewDebbuging` 값이 (으)로 설정됨 `Fals`기본적으로 e입니다. 활성화하려면 을 호출하십시오. `setWebContentsDebuggingEnabled(true)` 을 클릭합니다.

* **OpenSSL 및 Curl 버전 업그레이드**

   libcurl이 v7.57.0으로 업데이트되고 OpenSSL이 v1.0.2k로 업데이트되었습니다.

* VAST 응답 개체에 대한 앱 수준 액세스

   새 API 도입 `NetworkAdInfo::getVastXml()` 응용 프로그램에 대한 VAST 응답 개체의 액세스를 제공합니다.

**버전 2.5.3**

Android TVSDK v2.5.3에서는 다음 업데이트 및 API 변경 사항을 제공합니다.

* CRS를 사용하는 모든 TVSDK 고객은 Android에서 TVSDK 2.5.3.85 또는 최신 버전으로 앱을 업그레이드하는 것이 좋습니다. 기존 앱 구현의 드롭인 대체 기능이 됩니다. TVSDK 업그레이드 후 프록시 도구(예: Charles)에서 CRS 크리에이티브 URL 요청을 확인하고 경로의 호스트 이름 및 버전이 아래 샘플 URL 구조에서와 같이 반영되는지 확인합니다.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* 사용자 지정 가능한 TVSDK의 사용자 에이전트: 사용자 에이전트를 사용자 지정하기 위해 몇 가지 새로운 API를 추가했습니다.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Android 애플리케이션과 TVSDK 간의 쿠키 공유: 이제 Android TVSDK는 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간의 쿠키 액세스를 지원합니다. 이제 쿠키가 Java 쿠키 저장소에 노출되므로 기본 C++ 레이어에서 설정 및/또는 수정할 수 있습니다.

* API 변경 사항:

   * 새 이벤트 `CookiesUpdatedEvent` 가 추가됩니다. 쿠키가 업데이트되면 미디어 플레이어에서 발송됩니다.

   * 새 API가에 추가됩니다. `NetworkConfiguration::set/ getCustomUserAgent()` 사용자 지정 사용자 에이전트를 사용합니다.

   * 새 API가에 추가됩니다. `NetworkConfiguration::set/ getEncodedUrlForTracking` unsafe 문자의 인코딩을 강제 수행하려면.

   * 새 API가에 추가됩니다. `NetworkConfiguration::getNetworkDownVerificationUrl()` 장애 조치(failover) 시 네트워크 확인 URL 설정

   * 새 속성이에 추가됩니다. `TextFormat::treatSpaceAsAlphaNum` 캡션을 표시하는 동안 공백을 영숫자로 처리할지 여부를 정의합니다.

* 의 변경 사항 `SizeAvailableEvent`. 이전에는 `getHeight()` 및 `getWidth()` 방법 `SizeAvailableEvent` 미디어 형식에서 반환된 프레임 높이 및 프레임 너비를 반환하는 데 2.5.2에서 를 사용합니다. 이제 디코더가 각각 반환한 출력 높이와 출력 너비를 반환합니다.

* 버퍼링 동작 변경: 버퍼링 동작이 변경되었습니다. 버퍼가 비어 있는 경우 수행할 작업에 대해서는 앱 개발자에게 맡깁니다. 2.5.3은 버퍼 빈 상황에서 재생 버퍼 크기를 사용합니다.

**버전 2.5.2**

Android TVSDK v2.5.2에서는 중요한 버그 수정 및 몇 가지 API 변경 사항을 제공합니다.

**버전 2.5.1**

Android 2.5.1에서 릴리스된 중요한 새로운 기능입니다.

* **성능 향상 -** 새로운 TVSDK 2.5.1 아키텍처는 많은 성능 향상을 제공합니다. 타사 벤치마킹 연구의 통계를 기반으로 하는 이 새로운 아키텍처는 업계 평균에 비해 시작 시간을 5배 단축하고 프레임 드롭을 3.8배 줄였습니다.

* **VOD 및 라이브를 즉시 실행 -** 인스턴트 온 기능을 활성화하면 재생이 시작되기 전에 TVSDK가 미디어를 초기화하고 버퍼링합니다. 백그라운드에서 여러 MediaPlayerItemLoader 인스턴스를 동시에 실행할 수 있으므로 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서의 재생이 즉시 시작됩니다. TVSDK 2.5.1은 용 인스턴트 온도 지원합니다. **live** 스트림도 포함됩니다. 라이브 스트림은 라이브 창이 이동할 때 다시 버퍼링됩니다.

* **향상된 ABR 논리 -** 새로운 ABR 논리는 버퍼 길이, 버퍼 길이 변경률 및 측정된 대역폭을 기반으로 합니다. 이렇게 하면 ABR에서 대역폭이 변동할 때 올바른 비트율을 선택하고 버퍼 길이가 변하는 속도를 모니터링하여 비트율 전환이 실제로 발생하는 횟수를 최적화합니다.

* **부분 세그먼트 다운로드/하위 세그먼테이션 -** TVSDK는 가능한 한 빨리 재생을 시작하기 위해 각 조각의 크기를 더 줄입니다. ts 조각에는 2초마다 키 프레임이 있어야 합니다.

* **지연 광고 해결 -** TVSDK는 재생을 시작하기 전에 프리롤이 아닌 광고의 해결을 기다리지 않으므로 시작 시간이 줄어듭니다. 찾기 및 트릭 플레이와 같은 API는 모든 광고가 해결될 때까지 계속 허용되지 않습니다. CSAI와 함께 사용되는 VOD 스트림에 적용할 수 있습니다. 광고 해결이 완료될 때까지 찾기 및 빨리 돌기와 같은 작업은 허용되지 않습니다. 라이브 스트림의 경우 이 기능은 라이브 이벤트 중 광고 해결에 대해 활성화할 수 없습니다.

* **영구 네트워크 연결 -** 이 기능을 사용하면 TVSDK에서 영구 네트워크 연결의 내부 목록을 만들고 저장할 수 있습니다. 이러한 연결은 각 네트워크 요청에 대해 새 연결을 연 다음 나중에 삭제하는 대신 여러 요청에 재사용됩니다. 이렇게 하면 효율성이 높아지고 네트워킹 코드의 지연 시간이 줄어들어 재생 성능이 빨라집니다.
TVSDK가 연결을 열면 서버에 *keep-live* 연결. 일부 서버는 이 유형의 연결을 지원하지 않을 수 있습니다. 이 경우 TVSDK는 각 요청에 대해 다시 연결하는 것으로 대체됩니다. 또한 영구 연결은 기본적으로 켜져 있지만 TVSDK에는 이제 필요한 경우 앱이 영구 연결을 끌 수 있도록 구성 옵션이 있습니다.

* **병렬 다운로드 -** 비디오와 오디오를 시리즈가 아닌 병렬로 다운로드하면 시작 지연이 줄어듭니다. 이 기능을 사용하면 HLS 라이브 및 VOD 파일을 재생할 수 있고, 서버에서 사용 가능한 대역폭 사용을 최적화하고, 버퍼 언더런 상황에 도달할 확률을 낮추고, 다운로드와 재생 간의 지연을 최소화합니다.

* **병렬 광고 다운로드 -** TVSDK는 광고 브레이크를 누르기 전에 컨텐츠 재생과 동시에 광고를 미리 가져와서 광고 및 컨텐츠를 원활하게 재생할 수 있습니다.

* **재생**

* **MP4 컨텐츠 재생 -** TVSDK 내에서 재생하기 위해 MP4 짧은 클립을 다시 코딩할 필요가 없습니다.

   >[!NOTE]
   >
   >MP4 재생에는 ABR 전환, 트릭 재생, 광고 삽입, 지연 오디오 바인딩 및 하위 세그먼테이션이 지원되지 않습니다.

* **적응형 비트 전송률(ABR)을 사용한 트릭 플레이 -** 이 기능을 사용하면 TVSDK가 트릭 재생 모드에 있는 동안 iFrame 스트림 간을 전환할 수 있습니다. iFrame 이외의 프로필을 사용하여 더 낮은 속도에서 트릭 플레이를 수행할 수 있습니다.

* **매끄러운 트릭 플레이 -** 이러한 개선 사항은 사용자 경험을 향상시킵니다.

   * 대역폭 및 버퍼 프로필을 기반으로 트릭 재생 중 적응형 비트 전송률 및 프레임 전송률 선택

   * IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps 고속 재생을 만듭니다.

* **콘텐츠 보호**

   * **해상도 기반 출력 보호 -** 이 기능은 재생 제한을 특정 해상도에 연결하여 보다 세밀한 DRM 컨트롤을 제공합니다.

* **워크플로우 지원**

   * **직접 청구 통합 -** 이렇게 하면 청구 지표가 Adobe Analytics 백엔드에 전송되고, Adobe Primetime은 고객이 사용한 스트림에 대해 인증합니다.

   TVSDK는 고객 판매 계약을 준수하여 지표를 자동으로 수집하여 청구 목적에 필요한 주기적 사용 보고서를 생성합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림의 기간에 따라 콘텐츠 유형, 광고 삽입 활성화 플래그 및 drm 활성화 플래그와 같은 청구 지표를 Adobe Analytics Primetime 소유 보고서 세트에 보냅니다. 이 경우 고객의 자체 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하거나 여기에 포함되지 않습니다. 요청 시 이 청구 사용 보고서는 정기적으로 고객에게 전송됩니다. 사용량 청구만 지원하는 청구 기능의 첫 번째 단계입니다. 설명서에 설명된 API를 사용하여 판매 계약을 기반으로 구성할 수 있습니다. 이 기능은 기본적으로 활성화되어 있습니다. 이 기능을 끄려면 참조 플레이어 샘플을 참조하십시오.

   * **향상된 페일오버 지원 -** 호스트 서버, 재생 목록 파일 및 세그먼트의 실패에도 불구하고 중단 없는 재생을 계속하기 위해 구현된 추가 전략입니다.


* **광고**

   * **Moat 통합 -** Moat에서 광고 가시성 측정을 지원합니다.

   * **동반 배너 -** 컴패니언 배너는 선형 광고와 함께 표시되며, 광고가 종료된 후에도 보기에 계속 표시되는 경우가 많습니다. 이러한 배너는 html 유형(HTML 코드 조각) 또는 iframe 유형(iframe 페이지의 URL)일 수 있습니다.

* **분석**

   * **VHL 2.0 -** Adobe Analytics에 대한 사용 데이터의 자동 수집을 위해 최적화된 최신 비디오 하트비트 라이브러리(VHL) 통합입니다. 구현을 쉽게 하기 위해 API의 복잡성이 감소되었습니다. VHL 라이브러리 다운로드 [Android용 v2.0.0](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) libs 폴더에서 JAR 파일의 압축을 풉니다.

* **크기 사용 가능한 이벤트 리스너**

   * `getHeight()` 및 `getWidth()` 방법 `SizeAvailableEvent` 는 이제 출력을 높이와 너비로 각각 반환합니다. 디스플레이 종횡비는 다음과 같이 계산할 수 있습니다.

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      Sar 폭과 Sar 높이 측면에서의 스토리지 종횡비는 또한 프레임 폭과 프레임 높이를 계산하는 데 사용할 수 있습니다.

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **쿠키**

   * Android TVSDK는 이제 Android 애플리케이션의 CookieStore에 저장된 JAVA 쿠키에 대한 액세스를 지원합니다. 새 쿠키가 의 일부로 제공될 때마다 기록하도록 콜백 API(onCookiesUpdated)가 제공됩니다 **쿠키 설정** 응답 헤더. 이러한 쿠키는 CookieStore를 사용하여 특정 URI/도메인에 대한 쿠키 값을 설정하여 다른 URI/도메인에 사용되는 HttpCookie 목록으로 사용할 수 있습니다. 마찬가지로 TVSDK의 쿠키 값은 CookieStore 추가 API를 사용하여 업데이트됩니다.

## 기능 매트릭스 {#feature-matrix}

Android용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

아래 기능 테이블에서 &#39;Y&#39;는 기능이 현재 릴리스에서 지원됨을 나타냅니다.

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생(재생, 일시 중지, 찾기) | VOD + 라이브 | Y |
| FER - 일반 재생(재생, 일시 중지, 찾기) | VOD 재생 | Y |
| 광고가 재생될 때 찾기 | VOD + 라이브 | 지원되지 않음 |
| HEVC 재생 | VOD + 라이브 | fMP4 컨테이너만 |
| AC3 및 EAC3 | VOD + 라이브 | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | Y |
| 적응 비트 전송률 전환 논리 | VOD + 라이브 | Y |
| 오디오 전용 재생 | VOD + 라이브 | Y |
| 다중 CDN 지원 | VOD + 라이브 | 지원되지 않음 |
| 오디오 전용 미디어가 있는 광고 재생 | VOD + 라이브 | 지원되지 않음 |
| 폐쇄 캡션 - 608/708 | VOD + 라이브 | Y |
| 폐쇄 캡션 - WebVTT | VOD + 라이브 | Y |
| 매니페스트 장애 조치 | VOD + 라이브 | Y |
| 고급 페일오버 | VOD + 라이브 | Y |
| QoS 및 플레이어 알림 | VOD + 라이브 | Y |
| 쿠키 헤더 지원 | VOD + 라이브 | Y |
| 사용자 지정 HTTP 헤더 지원 | VOD + 라이브 | Y(허용 목록 필요) |
| 버퍼 제어 매개 변수 설정 | VOD + 라이브 | Y |
| 적응형 비트 전송률 제어 설정 | VOD + 라이브 | Y |
| 사용자 지정 매니페스트 태그 | VOD + 라이브 | Y |
| 지연 오디오 바인딩 | VOD + 라이브 | Y |
| 302 리디렉션 | VOD + 라이브 | Y |
| 오프셋이 있는 재생 | VOD + 라이브 | Y |
| 트릭 플레이 | VOD + 라이브 | Y |
| 트릭 플레이에서 슬로우 모션 | VOD + 라이브 | 지원되지 않음 |
| 부드러운 트릭 플레이(ABR 포함) | VOD + 라이브 | Y |
| ID3 구문 분석 | VOD + 라이브 | Y |
| 광고 일시 중단 | VOD + 라이브 | 지원되지 않음 |
| 즉시 사용 | VOD + 라이브 | 지원되지 않음 |
| 불연속 마커 지원 | VOD + 라이브 | Y |
| 302 리디렉션 고정 | VOD + 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생, 광고 활성화됨 | VOD + 라이브 | Y |
| 광고가 활성화된 FER 콘텐츠 | VOD | Y |
| 기본 광고 동작 | VOD + 라이브 | Y |
| VAST 2.0/3.0 | VOD + 라이브 | Y |
| VMAP 1.0 | VOD + 라이브 | Y |
| MP4 광고 | VOD + 라이브 | Y (CRS에서) |
| 광고가 활성화된 트릭 플레이 | VOD + 라이브 | Y |
| 광고만 | VOD | Y |
| 타깃팅 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 광고 동작 | VOD + 라이브 | Y |
| 사용자 지정 광고 태그 | 라이브 | Y |
| 사용자 지정 광고 해결자 | VOD + 라이브 | Y |
| Freewheel 사용자 지정 광고 해결 프로그램 | VOD | Y |
| C3 | VOD + 라이브 | 지원되지 않음 |
| 지연 광고 해결 | VOD | Y |
| 불연속 마커 지원 - SSAI | VOD + 라이브 | Y |
| 컴패니언 광고, 배너 광고 및 클릭 가능한 광고 | VOD + 라이브 | Y |
| VPAID 2.0 | VOD + 라이브 | Y (JS) |
| 초기 광고 종료 | 라이브 | Y |
| 규칙 기반 크리에이티브 우선 순위 지정 | VOD + 라이브 | Y |
| CRS 규칙 | VOD + 라이브 | Y |
| JSON 광고 해결자 | VOD + 라이브 | 지원되지 않음 |
| Moat 통합 | VOD + 라이브 | Y |
| 부분 광고 브레이크 삽입 | 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| AES 암호화 | VOD + 라이브 | Y |
| 샘플 AES 암호화 | VOD + 라이브 | Y |
| 토큰화된 스트림 | VOD + 라이브 | Y |
| 와이드빈 | VOD + 라이브 | fMP4 컨테이너만 |
| 프라임타임 DRM | VOD + 라이브 | Y |
| 외부 재생(RBOP) | VOD + 라이브 | Primetime DRM 전용 |
| 라이선스 회전 | VOD + 라이브 | Primetime DRM 전용 |
| 키 회전 | VOD + 라이브 | Primetime DRM 전용 |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| Adobe Analytics VHL 통합 | VOD + 라이브 | Y |
| 청구 | VOD + 라이브 | Y |

## 해결된 문제 {#resolved-issues}

해결이 보고된 문제와 관련이 있는 경우 Zendesk 참조가 표시됩니다(예: ZD#xxxxx).

**Android TVSDK 3.15**

이 섹션에서는 TVSDK 3.14 Android 릴리스에서 해결된 문제에 대한 요약을 제공합니다.

* ZD#46903 - 크리에이티브 태그가 없거나 다음과 같은 경우 애플리케이션이 여러 번 충돌합니다. [!UICONTROL url CDATA] 다음에서 비어 있음: [!UICONTROL VAST] 응답.

**Android TVSDK 3.14**

* ZD#46903 - 다음과 같은 경우 애플리케이션이 충돌합니다. [!UICONTROL CDATA] 노드가 다음 중 하나에 대해 비어 있음: [!UICONTROL ClickTracking], [!UICONTROL CustomClick] 또는 [!UICONTROL CompanionClickTracking] 의 요소 [!UICONTROL VAST] 응답.

### 이전 릴리스에서 해결된 문제

**Android TVSDK 3.12**

* ZD#40584 - Primetime 참조 앱이 최신 gradle 버전으로 빌드되지 않습니다.

**Android TVSDK 3.11**

* ZD#41252 - WebVTT의 한글 문자가 Android 7.1 이후에 깨졌습니다.

**Android TVSDK 3.10**

* ZD#40340 - 모든 TS(TypeScript) 파일을 차단 목록에 추가한 후 재생을 시도하면 &quot;앱이 응답하지 않음&quot; 오류가 발생하여 애플리케이션이 충돌합니다.

**Android TVSDK 3.8**

* 추가된 새 문제가 없습니다.

**Android TVSDK 3.7**

* 추가된 새 문제가 없습니다.

**Android TVSDK 3.6**

* 추가된 새 문제가 없습니다.

**버전 3.5**

* ZD#37503 - CRS 규칙에 대한 JSON 응답은 중복 요청을 방지하기 위해 캐시됩니다.

**버전 3.4**

* ZD#37996 - 선형 및 VOD CMAF HEVC 스트림에 대한 재생 저하 문제가 수정되었습니다.
* ZD#37706 - 잘못된 캡션 문제가 수정되었습니다.
* ZD#37622 - 특정 광고에 대한 치명적인 URISyntaxErrors 문제가 수정되었습니다.
* ZD#36938 - 비트율이 중간 비트율로 전환한 다음 트릭 플레이를 종료한 후 가장 높은 비트율로 선택하던 문제를 수정했습니다.

**버전 3.3**

* ZD#37394 - CMAF 에셋 빨리 감기는 속도 변경 후 아티팩트를 발생시킵니다.
   * 트릭 플레이 중에 프로필 변경과 함께 발생하는 문제를 수정했습니다.
* ZD#37396 - 일부 미드롤 및 포스트롤에 대해 광고 추적 이벤트가 누락되었습니다.
   * 광고 추적 이벤트에 대한 특정 사례를 수정했습니다.
* ZD#37491 - 오류 메타가 있는 HTTP 상태 코드가 없습니다.
   * 스택에서 네트워크 오류를 더 높게 전파하는 작업을 수행했습니다.
* ZD#37808 - 새 사용자 정의 헤더 허용 목록.
   * SSAI_TAG 지원이 이 수정 사항의 일부로 추가되었습니다.
* ZD#37622 - 특정 광고 포드에서 URISyntax 오류 발생.
   * 고객 Android 앱에 인코딩되지 않은 %가 포함된 광고가 제공될 때 스트림 재생 충돌에 대한 문제를 해결했습니다
* ZD#37631 - Android TVSDK용 기본 매니페스트 재시도 메커니즘.
   * 이 개선 사항을 처리하기 위해 네트워크 구성에 새 API가 추가되었습니다. 이 API를 사용하지 않으면 매니페스트가 다시 시도되지 않습니다. 이 옵션을 사용하면 네트워크 오류 및 시간 제한을 처리하기 위해 매니페스트가 다시 시도됩니다.

**버전 3.2**

* ZD#37493- 라이브 재생에 대한 추적 비콘은 시퀀스의 첫 번째 광고에 대해 간헐적으로 실행되지 않습니다.
* ZD#36985- 추적 비콘은 VMAP 응답의 빈 광고 브레이크에 대해 전송되지 않습니다.
* ZD#37134 - TVSDK에서 VMAP 응답에 대해 잘못된 ID가 간헐적으로 발생합니다.

**버전 3.0**

* ZD#33740 - TVSDK는 MediaPlayer 객체를 생성하고 replaceCurrentResource()를 호출한 직후에 불필요한 경고를 발생시킵니다.

   * 플레이어가 일시 중단된 상태에서만 복원을 호출하여 이전 수정 사항을 개선했습니다.

* ZD#36442 - 모든 새로운 재생은 원격 디버깅 세션을 연결 해제하여 디버깅할 수 없습니다.

   * 디버깅이 기본적으로 활성화되어 있지 않으므로 웹 보기에서 기본적으로 디버그를 수행할 수 없습니다. 필요할 경우 MediaPlayer.getCustomAdView()에서 반환된 객체에서 setWebContentsDebuggingEnabled(true)를 호출하여 앱을 디버깅할 수 있도록 설정해야 합니다.

* ZD#33688 - 적시 지원 및 해결

   * 광고 브레이크는 광고 브레이크의 위치 이전에 지정된 간격으로 해결됩니다.

* ZD#36441 - 라이브 기간 이 5분 이상 지속되면 여러 문제가 발생합니다.

   * 가상 라이브 포인트를 계산하는 동안 virtualStartTime이 두 번 추가되어 이 문제가 발생하는 문제가 해결되었습니다.

**Android TVSDK 2.5.6**

* ZD #34992 - 닫힌 캡션의 언어가 비어 있습니다.

   * TVSDK가 캡션 추적 세부 사항을 가져오기 위해 기본 매니페스트에서 #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS를 구문 분석하지 않는 경우가 수정되었습니다.

* ZD #35078 - Android P 유효성 검사.

   * TVSDK 2..5.6은 최신 Android P 베타 빌드로 유효성을 검사했습니다. 새 Android OS로 인해 발견된 문제가 없습니다.

* ZD #34149 - 플레이어는 오류가 발생하는 경우에도 매니페스트를 계속 요청합니다.

   * 모든 프로필이 다운된 경우에도 TVSDK가 반복해서 호출하는 경우가 해결되었습니다(404 오류).

* ZD #31533 - 앱이 백그라운드로 전송된 후 Android에서 오디오 재생.

   * 추가됨 `enableAudioPlaybackInBackground` 앱이 백그라운드에 있을 때 오디오 재생을 활성화하기 위해 인수로 &#39;True&#39;를 사용하여 호출해야 하는 MediaPlayer의 API입니다(플레이어가 준비됨 상태일 때).

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK는 실제 비디오 크기가 640x360일 때 640x368에 알립니다.

   * 변수 m_nOutputHeight(AndroidMCVideoDecoder 내부)가 실제 출력 높이 대신 프레임 높이로 업데이트되었습니다. m_nOutputHeight를 올바르게 계산하기 위해 getVideoFrame 함수에 관련 변경 사항이 적용되었습니다.

* ZD #26614 - 긴급 — 타사 광고 제공/프로그래밍 방식 — 노출 횟수 제공 실패.

   * &quot;공백&quot;이 &quot;같음&quot; 기호 앞에 있으면 문제가 재현될 수 있었던 XML 구문 분석의 사례를 처리하여 이전 수정 사항을 개선했습니다 &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: CRS 요청에 AdSystem 및 Creative ID를 추가합니다.

   * 이제 1401 및 1403 요청에 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 새 매개 변수로 포함합니다.

* ZD #33062 - TVSDK가 CDATA 노드 아래의 VAST 응답에 파이프 문자가 발생할 때 충돌합니다.

   * NetworkConfiguration 클래스의 API setEncodeUrlForTracking이 인코딩할 URL에서 안전하지 않은 문자로 제거되었습니다.

* ZD #33063 - CRS 파일 선택 로직이 손상되었습니다. - TVSDK가 webm 형식에 대한 CRS 요청을 보내지 않고 대신 3gpp 파일에 대해 보냅니다.

   * 이제 논리를 수정했습니다. Webm 및 3gpp 포맷이 있는 미디어 파일을 사용할 때, CRS 요청이 webm에 대해 전송될 것이다. 그리고 3gpp 포맷이 있는 미디어 파일들을 모두 사용할 때, 가장 높은 비트율 3gpp 파일에 대해 전송될 CRS 요청.

* ZD #33125 - Android 앱이 VMAP 내의 특정 DoubleClick 태그와 충돌합니다.

   * 충돌을 방지하기 위해 시나리오를 수정했습니다.

* ZD #32256 - 라이선스 회전 및 키 회전 문제 - Adobe 액세스

   * SampleAES 콘텐츠에 대한 DRM 메타데이터로 세그먼트 초기화를 수정했습니다. AES128 콘텐츠에서는 잘 작동합니다.

* ZD #33619 - 라이브 포인트 근처에서 버퍼링 상태에서 증가하는 재생 목록 콘텐츠가 보류됩니다.

   * 트릭 재생 모드에서 라이브 포인트를 교차할 때 사례를 처리했습니다

* ZD #34151 - TimedMetadata 개체의 순서가 잘못되었습니다.

   * 타임라인에서 같은 시간에 속할 경우 두 개의 TimedMetadata 이벤트가 임의의 순서로 표시되었습니다. 매니페스트에서 원래 순서를 유지했습니다.

* ZD #34189 - 광고 브레이크를 시작하려고 할 때 문제가 발생합니다.

   * 불연속성을 사용하여 결합된 SSAI 광고에 관한 문제였습니다. 그리고 그 원인은 우리가 그러한 광고의 시작을 찾을 때, 우리는 키프레임을 찾고 그것을 찾지 못하는 비헤이비어였습니다. 이유는 광고의 최소 오디오 타임스탬프가 최소 비디오 타임스탬프 이전이기 때문입니다. 따라서 잘못된 fragmentDump 데이터에서 키 프레임을 검색합니다. 이제 수정되었습니다.

* ZD #34528 - FireTV 3세대 동글에서 비디오 해상도가 640x360 이상으로 업그레이드되지 않음.

   * 최신 펌웨어 업데이트를 포함하도록 수정 사항을 개선했습니다.

* ZD #34793 - VideoEngine에서 auditudeSettings를 사용할 수 있다고 가정하고 있지 않은 경우, 일부 경우에 사용자 지정 콘텐츠 확인자와 충돌하는 데 사용된 TVSDK 2.5.x입니다.

   * Null 공유 포인터(auditudeSettings)에 대한 함수 호출로 인해 충돌이 발생했습니다. VideoEngineTimeline::placeToSourceTimeline() 내에 조건부 검사를 추가하여 해당 개체에 대해 모든 항목을 호출하기 전에 auditudeSettings를 사용할 수 있는지 확인했습니다.

* ZD #32584 - 의 전체 정보에 액세스할 수 없음 &lt;extensions> VAST 응답 노드.

   * XML 구문 분석 문제를 해결했습니다. 이제 NetworkAdInfo는 &lt;extensions> 노드

* ZD #35086 - 특정 VMAP 응답이 있는 경우 플레이어에서 전체 확장 데이터를 가져오지 않습니다.

   * 확장 xml에 특성 값 내에 큰따옴표가 있는 경우 XML 구문 분석이 작동하지 않아 확장 xml에만 문제가 있습니다. 문제를 해결했습니다.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Webview 원격 디버깅을 활성화하는 재생 세션입니다.

WebViewDebugging은 기본적으로 False로 설정되어 있습니다. 디버깅을 사용하려면 setWebContentsDebuggingEnabled(true)를 사용하여 응용 프로그램을 통해 true로 설정합니다.

* ZenDesk#33011 - CRS 요청이 실패하는 경우 광고 타임라인이 해결되지 않습니다.

   광고에 대한 CRS 요청이 실패하면 타임라인이 해결되고 나머지 광고가 재생됩니다.

* ZenDesk#34528 - FireTV 3세대 동글의 비디오 해상도가 640x360 이상으로 업그레이드되지 않습니다.

   비디오 해상도는 비트 전송률 스위치로 전환됩니다.

* ZenDesk#33192 - AudioUpdatedEventListener::onAudioUpdated를 통해 트랙을 검색할 때 AudioTrack에 Null 이름이 있습니다.

   FireTV Stick의 몇 가지 시나리오에서 실제 오디오 업데이트가 없을 때 onAudioUpdate 이벤트가 실행되었습니다. 이제 해결되었습니다.

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata 사용자 지정 태그 구독이 작동하지 않습니다.

   ID3 데이터를 바이트 배열(APIC 또는 일반 데이터를 지원하기 위해)로 클라이언트에 반환하는 반면, 1.4에서는 문자열을 반환합니다. 바이트 배열은 null 종료 문자 자체를 처리하지 않으므로 클라이언트에 특수 문자를 표시합니다. 이 문제는 현재 해결되었습니다.
* Zendesk#32670 - 플레이어가 중복 재생 목록으로 페일오버되지 않음

   이 기능은 현재 제대로 작동하며 setNetworkDownVerificationUrl은 예상대로 작동합니다.
* Zendesk#32369 - 닫힌 캡션은 다른 색상 가비지 또는 아티팩트를 보여줍니다.

   최신 빌드에서 CC 오류 문제가 수정되었습니다.
* Zendesk#25590 - 개선: TVSDK 쿠키 저장소(C++ ~ JAVA )

   Android TVSDK는 이제 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간 쿠키 액세스를 지원합니다.
* Zendesk#32252 - TVSDK_Android_2.5.2.12에는 PTPLAY-20269에 대한 수정 사항이 없는 것 같습니다.

   이 문제는 수정되었으며 2.5.2 분기로 통합되었습니다.
* Zendesk#31806 - Auditude는 준비에 집착합니다.

   응답 XML에 빈 태그가 있으므로 플레이어가 준비 중 상태에서 멈췄습니다. 이제 문제가 해결되었습니다.
* Zendesk#31727 - TVSDK 2.5 자막 문자가 삭제되거나 철자가 잘못되었습니다.

   문제가 수정되었으며 문자를 삭제/오기하지 않습니다.
* Zendesk#31485 - DrmManager in 2.5

   새 DrmManager(컨텍스트 컨텍스트)를 통해 DrmManager를 만드는 동안 문제가 발생했습니다. DRMManager를 제공하는 DRMService 클래스를 구현했습니다.
* Zendesk#32794- 1080P 해상도 스트림이 Android에서 재생되지 않음

   미디어 형식에서 반환된 프레임 높이 및 프레임 너비를 반환하는 데 사용되는 SizeAvailableEvent의 SizeAvailableEvent 이전, getHeight() 및 getWidth() 메서드를 2.5로 변경했습니다. 이제 디코더가 각각 반환한 출력 높이와 출력 너비를 반환합니다.
* Zendesk#19359 세트 수준 매니페스트에서 특성 위치#EXT-X-FAXS-CM 인해 Flash Player 충돌이 발생합니다.

   #EXT-X-FAXS-CM 태그는 항상 개별 비트율 또는 세그먼트가 재생 목록에 표시되기 전에 맨 위 재생 목록에 표시되어야 합니다.

**Android TVSDK 2.5.2**

* Zendesk#17305 불투명 배경이 있는 폐쇄 캡션의 아티팩트.

   TextFormat의 setTreatSpaceAsAlphaNum 속성이 표시됩니다. 속성은 기본적으로 False입니다. 클라이언트에서 속성을 True로 설정하여 다크 스페이스 문제를 해결합니다.

* Zendesk#25097 CC 디스플레이에는 CC 설정이 있는 시각적 아티팩트가 있습니다.

   TextFormat의 setTreatSpaceAsAlphaNum 속성이 표시됩니다. 속성은 기본적으로 False입니다. 클라이언트에서 속성을 True로 설정하여 다크 스페이스 문제를 해결합니다.

* Zendesk #31620 TVSDK 플레이어에서 나가는 사용자 에이전트 문자열이 잘렸습니다.

   사용자 에이전트 문자열은 128자 이후에 더 이상 잘리지 않습니다.

   Adobe Primetime 버전 문자열이 시스템 사용자 에이전트에 추가됩니다.

* Zendesk #30809 Missing SEEK_END 이벤트로 인해 앱이 재생 상태로 전환되지 않습니다.
* Zendesk #30415 Closed Caption의 &#39;Cyan&#39; 색상은 이제 이전 Primetime TVSDK 릴리스와 비교하여 더 어두운 색조의 파란색(청록색)입니다.

   색상이 짙은 청록색에서 청록색으로 변경됩니다.

* Zendesk #30727 VOD 광고가 다운로드/해결되지 않습니다.

   명시적 닫기 태그(&#39;)가 없는 빈 VAST 태그가 있는 경우 VMAP XML에서&lt;/vast>&#39;) 그리고 그 뒤에 줄바꿈 문자가 없으면 VMAP XML이 제대로 구문 분석되지 않고 광고가 재생되지 않을 수 있습니다.

**Android TVSDK 2.5.1**

* 장치별(Samsung Galaxy Tab 4) 충돌, 시청이 가능한 VOD DRM LBA 및 광고를 클릭합니다.
* VHL - 오프셋에서 콘텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생되면 VHL 하트비트가 이벤트를 호출합니다:type:재생 광고가 누락되었습니다.
* 완료 상태로 전환되면 플레이어는 포스트롤 광고에 대한 SKIP adBreakPolicy를 사용하여 재생 상태로 돌아갑니다.
* 나가는 광고 콜백에 쿠키가 첨부되지 않고 있습니다.
* 광고 큐 포인트는 표시되지 않습니다.
* 별도의 EAC3 SAP 트랙이 있는 HLS는 로드되지 않습니다.
* 미디어 플레이어가 복원된 후 TVSDK가 화면 켜기 의도를 수신하면 플레이어가 충돌합니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

**Android TVSDK 3.11**

* 새로운 제한 사항이 추가되지 않았습니다.

### 이전 릴리스의 알려진 문제 및 제한 사항

**Android TVSDK 3.10**

* 새로운 제한 사항이 추가되지 않았습니다.

**Android TVSDK 3.8**

* 새로운 제한 사항이 추가되지 않았습니다.

**Android TVSDK 3.7**

* 새로운 제한 사항이 추가되지 않았습니다.

**Android TVSDK 3.6**

* 새로운 제한 사항이 추가되지 않았습니다.

**Android TVSDK 3.5**

* 새로운 제한이 추가되지 않았습니다.

**Android TVSDK 3.4**

* ID3, 폐쇄 캡션, 지연 바인딩 오디오 지원은 CMAF(CBC) 스트림에 대해 확인되지 않았습니다.
* 일부 장치에서는 CMAF 스트림에서 트릭 플레이 중에 비디오 왜곡이 맨 위에 나타날 수 있는 낮은 재현성 문제가 있습니다.

**Android TVSDK 3.3**

* clcp:c608 캡션은 CMAF 스트림 재생에 지원되지 않습니다.

**Android TVSDK 3.2**

* TVSDK 3.2는 CMAF 샘플 AES 및 AES128 스트림 재생을 지원하지 않습니다.
* HEVC CMAF 스트림은 폐쇄 캡션 재생을 지원하지 않습니다.
* 암호화되지 않은 세그먼트 주변에서 찾기를 수행하면 WV 암호화된 스트림에 대해 녹색 색상이 나타납니다.
* CMAF 스트림은 ID3 이벤트를 지원하지 않습니다.
* HLS 스트림은 TTML 캡션 형식을 지원하지 않습니다.

**Android TVSDK 3.0**

* HEVC 지원에는 이번 릴리즈에서 다음과 같은 제한 사항이 있습니다

   * DRM은 지원되지 않음
   * CC (CEA 608/708) 지원이 확인되지 않음
   * 4K 지원이 아직 없습니다.
   * ID3 태그 지원이 확인되지 않음

* 광고 진행 이벤트의 경우 타임라인 바가 100% 정확한 광고 재생 시간을 반영하지 못할 수 있습니다. 해결 방법으로 다음을 사용할 수 있습니다. `adcompleteevent` 타임라인 표시줄 업데이트, 광고 관련 UI 제거 등과 같은 다양한 용도로 광고 재생 완료 및 업데이트 UI를 알 수 있습니다.
* VMAP에서 반환된 방대한 광고 호출은 Just-In-Time 조회 헤드 위치를 준수하지 않습니다.

**Android TVSDK 2.5.6**

* 여러 VMAP 광고 브레이크가 동시에 지원되지 않습니다.

**Android TVSDK 2.5.3**

이 버전에는 다음과 같은 문제가 있습니다.

* Live Video 재생에 저사양 장치 또는 네트워크 상태에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER도 작동하지 않습니다.
* 지연 바인딩 오디오 콘텐츠가 검색 상태일 때 재생이 중단될 수 있습니다.
* 간헐적으로 webVTT 캡션이 라이브 컨텐츠에 대해 동기화되지 않을 수 있습니다.
* 간헐적으로 광고 브레이크에서 나온 후 몇 개의 프레임이 빠르게 재생되는 것을 볼 수 있습니다.
* 광고가 재생되더라도 트리플 래퍼 광고 브레이크에 대해 303 오류가 발생하는 경우가 있습니다.

**Android TVSDK 2.5.2**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에는 로우 엔드 장치에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* VOD 미디어 종료를 시도할 때 재생이 가끔 지연될 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 offset이 있는 FER도 작동하지 않습니다.

**Android TVSDK 2.5.1**

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에 로우 엔드 장치에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 offset이 있는 FER도 작동하지 않습니다.
* VMAP XML에서 명시적 닫기 태그( )가 없는 빈 VAST 태그가 있는 경우&lt;/vast>), 그리고 그 뒤에 새 줄이 없으면 VMAP XML이 제대로 구문 분석되지 않고 광고가 재생되지 않을 수 있습니다.
* VPAID 포스트롤은 지원되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* [시스템 요구 사항](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Android 프로그래머용 TVSDK 3.10 안내서](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [API 참조용 TVSDK Android Javadoc](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API 문서](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - 각 Java 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 JavaDoc보다 더 많은 설명 자료가 포함되어 있으므로 Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.
* [Android(Java)용 TVSDK 1.4 - 2.5 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 화면 켜기/끄기 시나리오 처리에 대한 자세한 내용은 `Application_Changes_for_Screen_On_Off.pdf` 빌드에 포함된 파일입니다.
* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
