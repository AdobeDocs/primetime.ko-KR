---
title: Android용 TVSDK 3.10 릴리스 노트
seo-title: Android용 TVSDK 3.11 릴리스 노트
description: Android용 TVSDK 3.11 릴리스 정보에서는 TVSDK Android 3.10의 새로운 기능 또는 변경된 내용, 해결되고 알려진 문제 및 장치 문제를 설명합니다
seo-description: Android용 TVSDK 3.11 릴리스 정보에서는 TVSDK Android 3.11의 새로운 기능 또는 변경된 내용, 해결되고 알려진 문제 및 장치 문제를 설명합니다
uuid: 685d46f5-5a02-4741-af5c-91e91babd6f7
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 3a27379f-3cef-4ea3-bcae-21382dc1e9fd
translation-type: tm+mt
source-git-commit: 34ec714ec190e77a70bf4e966d6df02ec0c99cb3

---


# Android용 TVSDK 3.10 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 3.10 릴리스 노트에서는 TVSDK Android 3.10의 새로운 기능 또는 변경된 내용, 해결되고 알려진 문제 및 장치 문제를 설명합니다.

Android 참조 플레이어는 배포의 samples/ 디렉토리에 Android TVSDK에 포함되어 있습니다. 함께 제공되는 README.md 파일은 참조 플레이어를 구축하는 방법을 설명합니다.

>[!NOTE]
>
>릴리스와 함께 배포된 README.md에 설명된 대로 참조 플레이어를 성공적으로 구축하려면 다음을 수행해야 합니다.
>
>1. https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases에서 VideoHeartbeat.jar [다운로드](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Android v2.0.0용 VideoHeartbeat 라이브러리)
>1. VideoHeartbeat.jar를 libs/ 폴더에 추출합니다.
>



Android용 TVSDK는 이전 버전보다 향상된 많은 성능을 제공합니다. 고품질의 보기 환경을 제공하고 다중 CDN 지원을 제외한 버전 1.4의 모든 기능을 제공합니다.

지원되는 포괄적인 기능 및 지원되지 않는 기능은 릴리스 [노트의 기능](#feature-matrix) 매트릭스에 나와 있습니다.

**Android TVSDK 3.10**

이 릴리스는 [해결된 문제](#resolved-issues) 섹션에 언급된 주요 고객 문제를 수정하는 데 중점을 두었습니다.

<!-- ## New features {#new-features} -->

<!--
## Android TVSDK 3.11
**Protection System Specific Header (PSSH) Box fetching allowed**
TVSDK now allows fetching of Protection System Specific Header Box associated with current loaded Media Resource. New API `getPSSH()` has been added to `com.adobe.mediacore.drm.DRMManager`.
For more information, see [Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).
Top customer issues fixed in the current release are mentioned in [resolved issues](#resolved-issues) section. -->

### 이전 릴리스의 새로운 기능 및 개선 사항

**Android TVSDK 3.9**

* **HTTPS를 통한** 안전한 전달 - Android TVSDK 3.9는 HTTPS를 통한 안전한 전달 기능을 도입하여 탁월한 확장성 및 성능을 통해 안전하게 컨텐츠를 전달할 수 있습니다.

   HTTPS를 통한 보안 제공을 활성화하기 위해 새로운 API가 `NetworkConfiguration` 클래스에서 도입되었습니다.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **부분 광고 브레이크 기능을** 통한 프리롤 지원 - 향상된 TVSDK 3.8은 PABI(Partial Ad-Break) 기능을 사용하여 프리롤 광고를 지원합니다.

   사전 롤 광고가 재생된 다음 라이브 TV의 경험을 에뮬레이션하여 라이브 지점에서 컨텐츠가 재생됩니다.

**Android TVSDK 3.7**

* Widevine 테스트 내용의 경우 DRMManager `setMediaDrmCallback` 클래스의 새 API가 노출되어 MediaDrmCallback 인터페이스의 기본 구현을 재정의합니다.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* C++ `MediaPlayerEvent.ITEM_UPDATED` 레이어에서 처리되지 않는 AppCrash 오류가 수정되었습니다(Android 64비트).

**Android TVSDK 3.6**

* **64비트 요구** 사항을 위한 앱 강화 - 이제 기본 라이브러리가 `(libAVEAndroid.so)` 업그레이드되어 두 버전으로 제공됩니다. 기존 armeabi(32비트) 기본 라이브러리 위치가 에서 변경되었으며 추가 arm64-v8a(64비트) 라이브러리가 `/framework/Player to /framework/Player/armeabi``/framework/Player/arm64-v8a.`

**버전 3.5**

* **Just In Time Ad** Resolution - TVSDK 3.5는 타임라인에서 재생된 광고를 지원하지 않습니다.
* **오프라인 재생** 지원 - 사용자는 이제 오프라인 재생을 통해 디바이스에 비디오 컨텐츠를 다운로드하고 연결되어 있지 않을 때 시청할 수 있습니다. 자세한 내용은 &quot;Android를 사용한[오프라인 재생&quot;을](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)참조하십시오.

**버전 3.4**

* 이제 TVSDK는 CBC로 암호화된 및 일반 스트림을 위한 CMAF 스트림 재생을 지원합니다.

**버전 3.3**

* **API 변경 사항**

   * 네트워크 오류 및 시간 초과를 `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` 처리하기 위해 새 API가 추가되었습니다.
      * 여기서 (n)은 재시도 횟수입니다.

**버전 3.2**

* **병렬 광고 해상도 및 매니페스트 다운로드 지원**

   * TVSDK 3.2는 VMAP을 제외한 모든 광고 요청 및 광고 중단에 대한 순차적 해상도 대신 동시 해상도를 지원합니다.
   * 광고 중단의 모든 광고 매니페스트는 동시에 다운로드됩니다.
* **광고 해상도 및 매니페스트 다운로드 시간 초과에 대한 지원을 활성화했습니다.**

   * 이제 사용자는 전체 광고 해상도 및 매니페스트 다운로드에 대한 시간 초과 값을 설정할 수 있습니다.  VMAP의 경우 모든 광고 나누기가 순차적으로 해결되므로 시간 초과 값은 개별 광고 나누기에 적용됩니다.
* **AdvertisingMetadata 클래스에 새로운 API가 도입되었습니다.**

   * void setAdResolutionTimeout(int adResolutionTimeout)
   * int getAdResolutionTimeout()
   * void setAdManifestTimeout(int adManifestTimeout)
   * int getAdManifestTimeout()
* **AdvertisingMetadata 클래스에서 API 아래 제거됨:**

   * void setAdRequestTimeout(int adRequestTimeout)
   * int getAdRequestTimeout()
* **AC3/EAC3 오디오 코덱을 사용하여 스트림 재생 활성화**

   * void alwaysUseAC3OnSupportedDevices(boolean val)의 MediaPlayer 클래스
* **TVSDK는 암호화된 Widevine CTR을 위한 CMAF 및 일반 스트림 재생을 지원합니다.**
* **이제 4K HEVC 스트림의 재생이 지원됩니다.**
* **병렬 광고 호출 요청** - TVSDK는 이제 20개의 광고 호출 요청을 동시에 프리페치합니다.

**버전 3.0**

* **TVSDK 3.0은 HEVC(High Efficiency Video Coding) 스트림을 지원합니다.**

* **적시 - 광고 마커에 더 가까운 광고 해결**

   이제 레이지 광고 해결이 각 광고 나누기를 독립적으로 해결합니다. 이전에는 광고 해상도가 두 단계로 진행되었습니다.사전 롤은 재생 시작 전에 해결되었으며 재생 시작 후 모든 중간/후 롤 슬롯이 결합되었습니다. 이 향상된 기능을 사용하면 이제 광고 큐 포인트 이전의 특정 시간에 각 광고 나누기가 해결됩니다.

   **참고:이제 레이지 광고 해결이 기본적으로 비활성화되도록 변경되었으며 명시적으로 활성화해야 합니다.**

   이 광고 메타데이터와 관련된 지연된 *광고 로드 허용치를* 가져오기 위해 새 API가 AdvertisingMetadata::setDelayAdLoadingTolerance에 추가됩니다.\
   이제 PREPARATION 이후 즉시 검색 기능이 허용되므로 광고 브레이크에 대한 검색 결과는 검색 완료 전에 즉시 해결됩니다.\
   신호 모드 SERVER_MAP 및 MANIFEST_CUES가 지원됩니다.

   자세한 내용은 API 및 이벤트 변경에 대한 TVSDK 3.0 for Android 프로그래머 가이드를 참조하십시오.

* **최신`targetSdkVersion`버전으로 업데이트**

   19 `targetSdkVersion` 에서 27로 업데이트하면 원활하게 작동합니다.

* **이제 Placement.Type getPlacementType()이 인터페이스 TimelineMarker의 메서드입니다**

   이 메서드는 Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL 또는 Placement.Type.POST_ROLL의 배치 유형을 반환합니다. 광고 브레이크가 확인되지 않으면 TimelineMarker 인터페이스의 getDuration() 메서드가 0을 반환합니다.

**버전 2.5.6.**

* **TVSDK 2.5는 Android P를 지원합니다.**

* **백그라운드 오디오 활성화**

   앱이 전경 상태에서 백그라운드로 이동할 때 오디오 재생을 활성화하려면 플레이어가 준비 상태일 때 앱은 MediaPlayer의 `enableAudioPlaybackInBackground` API를 인수로 호출해야 합니다.

* **alwaysUseAudioOutputLatency(boolean val) in MediaPlayer class**

설정할 때 오디오 타임스탬프 계산에서 출력 지연을 사용합니다.
부울 매개 변수 val - True는 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

* **대역폭 속도가 갑자기 끊기는 경우에도 최적의 재생 환경을 제공할 수 있도록 최적화**

이제 TVSDK가 필요한 경우 진행 중인 세그먼트의 다운로드를 취소하고 해당 변환으로 동적으로 전환합니다. 이 작업은 중단 없이 비트 전송률을 원활하게 전환하여 수행할 수 있습니다.

**버전 2.5.5**

* **부분 광고 중단 삽입**

   부분적으로 시청된 광고에 대한 추적을 실행하지 않고 광고 중간에 참여하는 TV와 같은 경험.\
   예:사용자는 3개의 30초 광고로 구성된 90초 광고 중단의 중간(40초)에 참여합니다. 이것은 쉬는 시간에 두 번째 광고에서 10초입니다.

   * 나머지 기간(20초) 동안 두 번째 광고가 재생되고 세 번째 광고가 재생됩니다.
   * 부분 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기가 실행됩니다.

* **HTTPS를 통한 안전한 광고 로딩**

   Adobe Primetime은 https를 통해 Primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청할 수 있는 옵션을 제공합니다.

* **CRS 요청에 추가된 AdSystem 및 Creative Id**

   * 이제 1401 및 1403 요청에서 새 매개 변수로 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 포함합니다.

* **NetworkConfiguration 클래스의 API setEncodeUrlForTracking은 URL에서 안전하지 않은 문자를 인코딩해야 하므로 제거되었습니다** .

**버전 2.5.4**

Android TVSDK v2.5.4는 다음 업데이트 및 API 변경 사항을 제공합니다.

* WebViewDebuging에 대한 기본값 변경

   WebViewDebuging 값은 기본적으로 False로 설정됩니다. 이를 활성화하려면 애플리케이션에서 setWebContentsDebuggingEnabled(true)를 호출합니다.

* OpenSSL 및 Curl 버전 업그레이드

   v7.57.0으로 libcurl을 업데이트하고 OpenSSL을 v1.0.2k로 업데이트했습니다.

* VAST 응답 개체에 대한 앱 수준 액세스

   응용 프로그램에 대한 VAST 응답 개체에 대한 액세스를 제공하는 새로운 API NetworkAdInfo::getVastXml()을 도입했습니다.

**버전 2.5.3**

Android TVSDK v2.5.3은 다음 업데이트 및 API 변경 사항을 제공합니다.

* CRS 파섹 기존 앱 구현의 드롭인 대체입니다. TVSDK 업그레이드 후 프록시 도구에서 CRS 크리에이티브 URL 요청을 확인합니다(예:Charles)를 클릭하고 경로의 호스트 이름과 버전이 아래 샘플 URL 구조와 같이 반영되는지 확인합니다.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* 사용자 정의 가능한 TVSDK 사용자 에이전트:사용자 에이전트를 사용자 정의하기 위한 몇 가지 새로운 API를 추가했습니다.

   * setCustomUserAgent(문자열 값)
   * getCustomUserAgent()

* Android Application과 TVSDK 간 쿠키 공유:Android TVSDK는 이제 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간의 쿠키 액세스를 지원합니다. 이제 Java 쿠키 저장소에 노출되므로 기본 C++ 레이어에서 쿠키를 설정 및/또는 수정할 수 있습니다.
* API 변경 사항:

   * 새 이벤트 쿠키 UpdatedEvent가 추가됩니다. 쿠키가 업데이트될 때 미디어 플레이어에 의해 전달됩니다.

   * 사용자 지정 사용자 에이전트를 사용하기 위해 NetworkConfiguration::set/ getCustomUserAgent()에 새 API가 추가됩니다.

   * NetworkConfiguration::set/ getEncodedUrlForTracking에 새 API가 추가되어 안전하지 않은 문자를 강제로 인코딩합니다.

   * 장애 조치(failover)의 경우 네트워크 확인 URL을 설정하기 위해 새 API가 NetworkConfiguration::getNetworkDownVerificationUrl()에 추가됩니다.

   * 캡션을 표시할 때 공백을 영숫자로 처리할지 여부를 정의하는 새 속성이 TextFormat::treatSpaceAsAlphaNum에 추가됩니다.

* SizeAvailableEvent의 변경 사항:이전에는 SizeAvailableEvent의 getHeight() 및 getWidth() 메서드가 Frame 높이 및 프레임 너비를 반환하는 데 사용되었으며, 이 메서드는 미디어 형식으로 반환되었습니다. 이제 디코더에서 반환된 출력 높이와 출력 너비를 각각 반환합니다.

* 버퍼링 동작의 변경 사항:버퍼링 동작이 변경되었습니다. 버퍼가 비어 있는 경우 원하는 작업을 앱 개발자에게 맡겼다. 2.5.3은 버퍼 빈 상황에서 재생 버퍼 크기를 사용합니다.

**버전 2.5.2**

Android TVSDK v2.5.2는 중요한 버그 수정 및 몇 가지 API 변경 사항을 제공합니다.

**버전 2.5.1**

Android 2.5.1에서 릴리스된 중요한 새로운 기능

* **성능**&#x200B;개선 새로운 TVSDK 2.5.1 아키텍처는 많은 성능 향상을 가져왔습니다. 타사 벤치마크 조사 결과를 바탕으로 새 아키텍처는 시작 시간을 5배 줄이고 업계 평균과 비교하여 드롭된 프레임을 3.8배 더 적게 제공합니다.

   * **VOD 및 실시간 실시간** 실시간 지원 - 인스턴트 온 경우 TVSDK가 초기화되고 재생이 시작되기 전에 미디어를 버퍼링합니다. 백그라운드에서 여러 MediaPlayerItemLoader 인스턴스를 동시에 실행할 수 있으므로 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 재생이 즉시 시작됩니다. 또한 TVSDK 2.5.1은 **실시간** 스트림을 위해 Instant On을 지원합니다. 라이브 윈도우를 이동하면 라이브 스트림이 다시 버퍼링됩니다.

   * **향상된 ABR 논리 -** 새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 비율 및 측정된 대역폭을 기반으로 합니다. 따라서 ABR은 대역폭 변동 시 올바른 비트 전송률을 선택하고 버퍼 길이 변경되는 속도를 모니터링하여 비트율 전환이 실제로 발생하는 횟수를 최적화합니다.

   * **부분 세그먼트 다운로드/하위 세그멘테이션 - TVSDK는** 가능한 한 빨리 재생을 시작할 수 있도록 각 조각 크기를 추가로 줄입니다. 조각 조각에는 2초마다 키 프레임이 있어야 합니다.

   * **레이지 광고 해상도 - TVSDK는** 재생을 시작하기 전에 비프리롤 광고의 해상도를 기다리지 않으므로 시작 시간을 단축할 수 있습니다. 검색 및 트릭 플레이와 같은 API는 모든 광고가 해결될 때까지 허용되지 않습니다. CSAI와 함께 사용되는 VOD 스트림에 적용됩니다. 검색 및 빨리 감기 등의 작업은 광고 해상도가 완료될 때까지 허용되지 않습니다. 라이브 스트림의 경우 라이브 이벤트 중에는 이 기능을 광고 해상도에 사용할 수 없습니다.

   * **영구 네트워크 연결 - 이** 기능을 통해 TVSDK는 영구 네트워크 연결의 내부 목록을 만들고 저장할 수 있습니다. 이러한 연결은 각 네트워크 요청에 대해 새 연결을 열고 이후에 삭제하는 대신 여러 요청에 대해 다시 사용됩니다. 이렇게 하면 네트워킹 코드의 효율성을 높이고 지연을 줄임으로써 재생 성능이 빨라집니다.
TVSDK가 연결을 열면 서버에 *지속적인* 연결을 요청합니다. 일부 서버에서는 이 유형의 연결을 지원하지 않을 수 있습니다. 이 경우 TVSDK가 각 요청에 대한 연결을 다시 설정하는 데 실패합니다. 또한 영구 연결은 기본적으로 켜져 있지만 TVSDK에는 앱이 원하는 경우 영구 연결을 끌 수 있는 구성 옵션이 있습니다.

   * **병렬 다운로드 -** 비디오 및 오디오를 연속적으로 다운로드하는 것이 시작 지연을 줄여줍니다. 이 기능을 사용하면 HLS Live 및 VOD 파일을 재생할 수 있고, 서버의 사용 가능한 대역폭 사용을 최적화하고, 버퍼 언더런 상황에 진입할 가능성을 낮추며, 다운로드와 재생 사이의 지연을 최소화할 수 있습니다.

   * **병렬 광고 다운로드 - TVSDK는 광고 중단이 발생하기 전에 컨텐츠 재생과 동시에 광고를 프리페치하므로 광고 및 컨텐츠를 매끄럽게 재생할 수 있습니다** .

* **재생**

   * **MP4 컨텐츠 재생 - TV** SDK에서 재생할 수 있도록 MP4 단편 클립을 다시 코딩할 필요가 없습니다.
      > [!NOTE]
      >
      > MP4 재생에는 ABR 전환, 트릭 재생, 광고 삽입, 늦은 오디오 바인딩 및 하위 세그멘테이션이 지원되지 않습니다.

   * **ABR(Trick Play with adaptive bit rate)** - 이 기능을 사용하면 TVSDK가 트릭 재생 모드에서 iFrame 스트림 간을 전환할 수 있습니다. iFrame이 아닌 프로파일을 사용하여 보다 빠른 속도로 trick을 재생할 수 있습니다.

   * **원활한 트릭 재생 - 향상된** 이러한 기능을 통해 사용자 경험을 향상시킬 수 있습니다.

      * 트릭 재생 중에 대역폭 및 버퍼 프로파일을 기반으로 적응 비트 전송률 및 프레임 속도를 선택할 수 있습니다.

      * IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps를 빠르게 재생할 수 있습니다.

* **컨텐츠 보호**

   * **해상도 기반 출력 보호 - 이** 기능은 재생 제한을 특정 해상도에 연결하여 보다 정교해진 DRM 컨트롤을 제공합니다.

* **워크플로우 지원**

   * **직접 청구 통합 - 이** 서비스는 Adobe Analytics 백엔드로 청구 지표를 전송하며, 이는 고객이 사용하는 스트림에 대해 Adobe Primetime에서 인증한 것입니다.
   TVSDK는 고객 판매 계약을 준수하면서 자동으로 지표를 수집하여 청구 목적에 필요한 주기적인 사용 보고서를 생성합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림 기간에 따라 콘텐츠 유형, 광고 삽입 가능 플래그, drm 활성화 플래그 등의 청구 지표를 Adobe Analytics Primetime 소유 보고서 세트로 전송합니다. 이 경우 고객의 자체 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하거나 포함시키지 않습니다. 요청 시 이 청구 사용량 보고서는 고객에게 정기적으로 전송됩니다. 이 단계는 비용 청구를 지원하는 첫 번째 청구 기능입니다. 설명서에 설명된 API를 사용하여 판매 계약에 따라 구성할 수 있습니다. 이 기능은 기본적으로 활성화되어 있습니다. 이 기능을 끄려면 참조 플레이어 샘플을 참조하십시오.

   * **향상된 장애 조치 지원 - 호스트 서버, 재생 목록 파일 및 세그먼트에 장애가 발생하더라도 중단 없이 계속 재생할 수 있도록 구현된 추가 전략입니다** .


* **광고**

   * **해자 통합 - 해자에서** 광고 시청 가능성 측정을 지원합니다.

   * **Companion banners - Companion 배너는 선형 광고와 함께 표시되며, 광고가 끝난 후에도 계속 표시됩니다** . 이러한 배너는 html(HTML 조각) 유형이거나 iframe(iframe 페이지의 URL)을 입력할 수 있습니다.

* **분석**

   * **VHL 2.0 - Adobe** Analytics에 대한 사용 데이터 자동 수집을 위해 최적화된 최신 VHL(Video Heartbeats Library) 통합입니다. 구현을 용이하게 하기 위해 API의 복잡도가 감소되었습니다. Android용 VHL 라이브러리 [v2.0.0을](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) 다운로드하고 libs 폴더에서 JAR 파일을 추출합니다.

* **SizeAvalableEventListener**

   * `getHeight()` 의 `getWidth()` 메서드는 `SizeAvailableEvent` 이제 각각 높이와 너비로 출력물을 반환합니다. 디스플레이 종횡비는 다음과 같이 계산할 수 있습니다.

      SizeAvailableEvent e;DAR = e.getWidth()/ e.getHeight();

      Sar 폭 및 Sar 높이 측면에서 저장 종횡비를 사용하여 프레임 폭과 프레임 높이를 계산할 수도 있습니다.

      SAR = e.getSarWidth()/e.getSarHeight();frameHeight = e.getHeight();frameWidth = e.getWidth()/SAR 파섹

* **쿠키**

   * Android TVSDK는 이제 Android 애플리케이션의 CookieStore에 저장된 JAVA 쿠키에 대한 액세스를 지원합니다. 새 쿠키가 &quot;Set-Cookie&quot; 응답 헤더의 일부로 올 때마다 기록하기 위해 콜백 API(onCookiesUpdated)가 제공됩니다. 이러한 쿠키는 CookieStore를 사용하여 특정 URI/도메인에 이러한 쿠키 값을 설정하여 다른 URI/도메인에 사용되는 HttpCookie 목록 형식으로 사용할 수 있습니다. 마찬가지로 TVSDK의 쿠키 값은 CookieStore 추가 API를 사용하여 업데이트됩니다.

## Feature Matrix {#feature-matrix}

Android용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

아래 기능 표에서 &#39;Y&#39;는 현재 릴리스에서 기능이 지원됨을 나타냅니다.

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생(재생, 일시 중지, 검색) | VOD + 라이브 | Y |
| FER - 일반 재생(재생, 일시 중지, 검색) | FER VOD | Y |
| 광고 재생 시간 검색 | 라이브 | 지원되지 않음 |
| AC3 | VOD + 라이브 | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | Y |
| 적응형 비트 전송률 전환 논리 | VOD + 라이브 | Y |
| 오디오 전용 재생 | VOD + 라이브 | Y |
| 다중 CDN 지원 | VOD + 라이브 | 지원되지 않음 |
| 오디오 전용 미디어를 사용한 광고 재생 | VOD + 라이브 | 지원되지 않음 |
| 자막 - 608/708 | VOD + 라이브 | Y |
| 자막 - WebVTT | VOD + 라이브 | Y |
| 매니페스트 장애 조치(Manifest Failover) | VOD + 라이브 | Y |
| 고급 장애 조치 | VOD + 라이브 | Y |
| QoS 및 플레이어 알림 | VOD + 라이브 | Y |
| 쿠키 헤더 지원 | VOD + 라이브 | Y |
| 사용자 정의 HTTP 헤더 지원 | VOD + 라이브 | Y(화이트리스트 필요) |
| 버퍼 컨트롤 매개 변수 설정 | VOD + 라이브 | Y |
| 적응형 비트 전송률 컨트롤 설정 | VOD + 라이브 | Y |
| 사용자 지정 매니페스트 태그 | VOD + 라이브 | Y |
| 늦은 오디오 바인딩 | VOD + 라이브 | Y |
| 302 리디렉션 | VOD + 라이브 | Y |
| 오프셋을 사용한 재생 | VOD + 라이브 | Y |
| 오디오 전용 재생 | VOD + 라이브 | Y |
| 트릭 플레이 | VOD + 라이브 | Y |
| 트릭 플레이의 슬로우 모션 | VOD + 라이브 | 지원되지 않음 |
| 부드러운 트릭 재생(ABR 사용) | VOD + 라이브 | Y |
| ID3 구문 분석 | VOD + 라이브 | Y |
| 광고 중단 | VOD + 라이브 | 지원되지 않음 |
| 즉시 켜기 | VOD + 라이브 | 지원되지 않음 |
| 비연속성 마커 지원 | VOD + 라이브 | Y |
| 302 리디렉션 지속 | VOD + 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생, 광고 활성화 | VOD + 라이브 | Y |
| 광고가 활성화된 FER 컨텐츠 | VOD | Y |
| 기본 광고 동작 | VOD + 라이브 | Y |
| VAST 2.0/3.0 | VOD + 라이브 | Y |
| VMAP 1.0 | VOD + 라이브 | Y |
| MP4 광고 | VOD + 라이브 | Y(CRS) |
| 광고를 사용하여 트릭 재생 | VOD + 라이브 | Y |
| 광고 전용 | VOD | Y |
| 타깃팅 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 광고 동작 | VOD + 라이브 | Y |
| 사용자 지정 광고 태그 | 라이브 | Y |
| 사용자 지정 광고 해상도 | VOD + 라이브 | Y |
| Freewheel 사용자 지정 광고 확인자 | VOD | Y |
| C3 | VOD + 라이브 | 지원되지 않음 |
| 레이지 광고 해결 | VOD | Y |
| 불연속 마커 지원 - SSAI | VOD + 라이브 | Y |
| 컴패니언 광고, 배너 광고 및 클릭 가능한 광고 | VOD + 라이브 | Y |
| VPAID 2.0 | VOD + 라이브 | Y(JS) |
| 조기 광고 종료 | 라이브 | Y |
| 규칙 기반의 크리에이티브 우선 순위 | VOD + 라이브 | Y |
| CRS 규칙 | VOD + 라이브 | Y |
| JSON 광고 해결 프로그램 | VOD + 라이브 | 지원되지 않음 |
| 해자 통합 | VOD + 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| AES 암호화 | VOD + 라이브 | Y |
| 샘플 AES 암호화 | VOD + 라이브 | Y |
| 토큰화된 스트림 | VOD + 라이브 | Y |
| DRM | VOD + 라이브 | Primetime DRM만 해당(향후:Widevine) |
| 외부 재생(RBOP) | VOD + 라이브 | Primetime DRM만 해당 |
| 라이선스 순환 | VOD + 라이브 | Primetime DRM만 해당 |
| 키 회전 | VOD + 라이브 | Primetime DRM 및 Widevine DRM |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| Adobe Analytics VHL 통합 | VOD + 라이브 | Y |
| 청구 | VOD + 라이브 | Y |

## 해결된 문제 {#resolved-issues}

해상도가 보고된 문제와 연결된 경우 ZD#xxxxx와 같은 Zendesk 참조가 표시됩니다.

**Android TVSDK 3.10**

* ZD#40340 - 모든 TS(TypeScript) 파일을 블랙리스트로 표시한 후 재생을 시도할 때 &quot;App Not Responding&quot; 오류가 발생하여 애플리케이션이 충돌합니다.

<!-- **Android TVSDK 3.11**
This section provides a summary of the issue resolved in TVSDK 3.11 Android release.
* ZD#41252 - Korean characters are displayed as missing glyph symbols for HLS manifests with WebVTT in Android TVSDK reference app. -->

### 이전 릴리스의 해결된 문제

**Android TVSDK 3.8**

* 추가된 새 문제가 없습니다.

**Android TVSDK 3.7**

* 추가된 새 문제가 없습니다.

**Android TVSDK 3.6**

* 추가된 새 문제가 없습니다.

**버전 3.5**

* ZD#37503 - CRS 규칙에 대한 JSON 응답은 중복 요청을 방지하기 위해 캐시됩니다.

**버전 3.4**

* ZD#37996 - 선형 및 VOD CMAF HEVC 파섹 스트림의 끊김 재생 문제가 해결되었습니다.
* ZD#37706 - 알아볼 수 없는 캡션 문제를 수정했습니다.
* ZD#37622 - 특정 광고에 대한 치명적인 URISyncErrors 문제를 수정했습니다.
* ZD#36938 - 비트 전송률을 중간 비트 전송률로 전환한 다음 트릭 플레이에서 벗어난 후 가장 높은 비트 전송률로 전환하는 문제를 수정했습니다.

**버전 3.3**

* ZD#37394 - CMAF 에셋을 빠르게 전달하면 속도가 변경된 후 아티팩트가 발생합니다.
   * 트릭 재생 중 프로필 변경 시 발생하는 문제를 수정했습니다.
* ZD#37396 - 일부 mid-rols 및 포스트롤에 대한 광고 추적 이벤트가 없습니다.
   * 광고 추적 이벤트에 대한 특정 사례를 수정했습니다.
* ZD#37491 - 오류 메타데이터가 있는 HTTP 상태 코드가 없습니다.
   * 스택에서 더 높은 네트워크 오류를 전파하는 작업이 수행되었습니다.
* ZD 파섹#37808 - 새 사용자 정의 헤더 허용
   * 이 수정의 일부로 SSAI_TAG 지원이 추가되었습니다.
* ZD#37622 - URIS특정 광고 창에서 세금 오류 동기화
   * 고객 Android 앱이 인코딩되지 않은 % 광고를 제공하는 경우 스트림 재생 충돌 문제가 해결되었습니다.
* ZD#37631 - Android TVSDK에 대한 마스터 매니페스트 재시도 메커니즘.
   * 이 개선 사항을 처리하기 위해 네트워크 구성에 새 API를 추가했습니다. 이 API를 사용하지 않으면 매니페스트가 다시 시도되지 않습니다. 이 매개 변수를 사용하는 경우 네트워크 오류 및 시간 초과를 처리하기 위해 매니페스트를 다시 시도합니다.

**버전 3.2**

* ZD#37493- 실시간 재생을 위한 추적 비콘이 시퀀스의 첫 번째 광고에 대해 간헐적으로 실행되지 않습니다.
* ZD#36985- VMAP 응답에서 빈 광고 중단에 대해 추적 비콘이 전송되지 않습니다.
* ZD#37134 - TVSDK가 간헐적으로 VMAP 응답에 대해 잘못된 ID를 throw합니다.

**버전 3.0**

* ZD#33740 - TVSDK 파섹

   * 플레이어가 일시 중단 상태일 때만 복원을 호출하여 이전 수정 사항을 개선했습니다.

* ZD#36442 - 모든 새로운 재생 시 원격 디버깅 세션이 끊겨 디버깅할 수 없습니다.

   * 디버깅이 기본적으로 활성화되어 있지 않으므로 웹 보기에서는 디버깅을 기본적으로 수행할 수 없습니다. MediaPlayer.getCustomAdView()에서 반환되는 개체에 대해 setWebContentsDebuggingEnabled(true)를 호출하여 필요한 경우 응용 프로그램에서 디버깅을 활성화해야 합니다.

* ZD#33688 - 적시에 지원 및 해결

   * 광고 브레이크는 광고 브레이크의 위치 전에 지정된 간격으로 해결됩니다.

* ZD#36441 - 라이브 창의 지속 시간이 5분 이상으로 계속 증가하여 여러 문제가 발생했습니다.

   * 가상 라이브 포인트를 계산하는 동안 virtualStartTime이 두 번 추가되어 이 문제가 발생하는 문제를 해결했습니다.

**Android TVSDK 2.5.6**

* ZD #34992 - 닫힌 캡션에서 언어가 비어 있습니다.

   * TVSDK가 캡션 추적 세부 정보를 가져오기 위해 기본 매니페스트에서 #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS를 구문 분석하지 않는 문제를 해결했습니다.

* ZD #35078 - Android P 유효성 검사.

   * TVSDK 2.5.6은 최신 Android P 베타 빌드로 확인되었습니다. 새로운 Android OS로 인해 발견된 문제가 없습니다.

* ZD #34149 - 오류가 발생하더라도 플레이어가 매니페스트를 계속 요청합니다.

   * 모든 프로필이 다운된 경우에도(404 오류) TVSDK가 반복적인 호출을 하는 문제를 해결했습니다.

* ZD #31533 - 앱이 백그라운드로 전송된 후 Android에서 오디오 재생

   * 앱이 백그라운드에 있을 `enableAudioPlaybackInBackground` 때 오디오를 재생할 수 있도록 &#39;True&#39;로 호출해야 하는 MediaPlayer의 API를 추가했습니다(플레이어가 준비 상태일 때).

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK는 실제 비디오 크기가 640x360이면 640x368에 알립니다.

   * m_nOutputHeight 변수(AndroidMCVideoDecoder 내부)가 실제 출력 높이 대신 프레임 높이로 업데이트됩니다. getVideoFrame 함수에서 m_nOutputHeight를 올바르게 계산하기 위해 관련 있는 변경을 수행했습니다.

* ZD #26614 - 긴급 — 서드파티 광고 서비스 / 프로그래머틱 광고 서비스 — 노출 횟수 서비스 실패

   * &quot;space&quot;가 &lt;VAST 버전 =&quot;2.0&quot;>과 같은 &quot;equal&quot; 기호 앞에 있을 때 문제가 재현될 경우 XML 구문 분석에서 사례를 처리하여 이전 수정 사항을 개선했습니다.

* ZD #29296 - Android:CRS 요청에 AdSystem 및 Creative ID 추가

   * 이제 1401 및 1403 요청에서 새 매개 변수로 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 포함합니다.

* ZD #33062 - CDATA 노드의 VAST 응답에서 파이프 문자가 발생할 때 TVSDK 충돌

   * NetworkConfiguration 클래스의 API setEncodeUrlForTracking이 인코딩할 URL의 안전하지 않은 문자로 제거되었습니다.

* ZD #33063 - CRS 파일 선택 로직이 손상되었습니다. - TVSDK가 웹 m 포맷에 대한 CRS 요청을 보내지 않고 대신 3gpp 파일에 대해 전송했습니다.

   * 이제 논리를 수정했습니다. webm 및 3gpp 형식의 미디어 파일을 사용하는 경우 웹에 대한 CRS 요청을 보냅니다. 또한 3gpp 형식의 미디어 파일을 모두 사용하는 경우 최고 비트 전송률 3gpp 파일에 대해 CRS 요청을 전송합니다.

* ZD #33125 - Android 앱이 VMAP 내의 특정 DoubleClick 태그와 충돌합니다.

   * 충돌을 방지하기 위해 시나리오를 수정했습니다.

* ZD 파섹 #32256 - 라이센스 순환 및 키 순환 문제 - Adobe Access

   * SampleAES 컨텐츠에 대한 DRM 메타데이터로 세그먼트 초기화를 수정했습니다. AES128 컨텐츠와 완벽하게 호환됩니다.

* ZD #33619 - 라이브 포인트 근처의 버퍼링 상태에서 계속 증가하는 재생 목록 컨텐츠를 빠르게 전달합니다.

   * 트릭 재생 모드에서 라이브 포인트를 넘을 때 이 문제가 해결되었습니다.

* ZD #34151 - TimedMetadata 개체의 순서가 잘못되었습니다.

   * 타임라인에서 두 개의 TimedMetadata 이벤트가 같은 시간에 속했다면 임의의 순서로 표시되었습니다. 원래 순서를 분명히 유지합니다.

* ZD #34189 - 광고 중단 시작을 찾는 경우 문제가 발생합니다.

   * 그 문제는 불연속성을 사용하여 봉합된 SSAI 광고와 관련된 것이었다. 그 원인은 우리가 그러한 광고의 시작 부분을 찾고자 할 때, 키프레임을 찾지만 찾지 못하는 행동이었습니다. 그 이유는 최소 비디오 타임스탬프 앞에 있는 광고의 최소 오디오 타임스탬프였습니다. 따라서 잘못된 fragmentDump 데이터에서 키 프레임을 검색합니다. 수정했습니다.

* ZD #34528 - FireTV 3세대 동글의 경우 비디오 해상도가 640x360을 초과하지 않습니다.

   * 최신 펌웨어 업데이트를 포함하도록 수정 사항 개선

* ZD #34793 - VideoEngine이 auditudeSettings를 사용할 수 있고 사용할 수 없다고 가정할 때 경우에 따라 TVSDK 2.5.x가 사용자 정의 컨텐츠 확인자와 충돌했습니다.

   * Null 공유 포인터(auditudeSettings)에 대한 함수 호출로 인해 충돌이 발생했습니다. VideoEngineTimeline::placeToSourceTimeline() 내에 조건부 검사를 추가하여 해당 개체에 대해 모든 것을 호출하기 전에 auditudeSettings를 사용할 수 있도록 했습니다.

* ZD #32584 - VAST 응답의 &lt;확장> 노드에 있는 전체 정보에 액세스할 수 없습니다.

   * XML 구문 분석 문제를 수정했으며 이제 NetworkAdInfo가 &lt;확장> 노드에 있는 전체 정보를 제공합니다.

* ZD #35086 - 특정 VMAP 응답 시 플레이어에서 전체 확장 데이터를 가져오지 않습니다.

   * 확장 xml에 특성 값 내에 큰 따옴표가 있는 경우 XML 구문 분석이 작동하지 않으므로 확장 xml에 문제가 있었습니다. 문제를 수정했습니다.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Playback session enabling webview remote debugging.

WebViewDebuging은 기본적으로 False로 설정됩니다. 디버깅을 사용하려면 setWebContentsDebuggingEnabled(true)를 사용하여 응용 프로그램을 통해 true로 설정합니다.

* ZenDesk#33011 - CRS 요청이 실패한 경우 광고 타임라인이 확인되지 않습니다.

   광고에 대한 CRS 요청이 실패하면 타임라인이 해결되고 나머지 광고가 재생됩니다.

* ZenDesk#34528 - FireTV 3세대 동글의 경우 비디오 해상도가 640x360 이상으로 업그레이드되지 않습니다.

   비디오 해상도는 비트 전송률 스위치로 전환됩니다.

* ZenDesk#33192 - AudioUpdatedEventListener::onAudioUpdated를 통해 트랙을 검색할 때 AudioTrack의 이름이 null입니다.

   FireTV Stick의 몇 가지 시나리오에서 실제 오디오 업데이트가 없을 때 onAudioUpdate 이벤트가 실행되었습니다. 이제 수정되었습니다.

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata 사용자 정의 태그 구독이 작동하지 않습니다.

   ID3 데이터를 바이트 배열로 반환(APIC 또는 일반 데이터 지원)하는 반면 1.4 반환 문자열은 클라이언트에 반환합니다. 바이트 배열은 null 종료 문자 자체를 처리하지 않으므로 클라이언트에 특수 문자를 표시했습니다. 이제 이 문제가 해결되었습니다.
* Zendesk#32670 - Player Not Failed Over To Redundant Playlist

   이제 제대로 작동하며 setNetworkDownVerificationUrl이 예상대로 작동합니다.
* Zendesk#32369 - 닫힌 캡션은 다른 색상 가비지 또는 결함을 표시합니다.

   최신 빌드에서 CC 결함 문제가 해결되었습니다.
* Zendesk#25590 - 개선:TVSDK 쿠키 저장소(C++에서 JAVA로)

   Android TVSDK는 이제 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간의 쿠키 액세스를 지원합니다.
* Zendesk#32252 - TVSDK_Android_2.5.2.12는 PTPLAY-20269에 대한 수정 사항이 없는 것 같습니다.

   이 문제는 수정되었으며 2.5.2 분기로 통합되었습니다.
* Zendesk#31806 - PREPARING의 Auditude 막대기

   응답 xml에 빈 태그가 있기 때문에 플레이어가 준비 상태에 있습니다. 이제 문제가 해결되었습니다.
* Zendesk#31727 - TVSDK 2.5 자막 문자가 삭제되거나 맞춤법이 잘못되었습니다.

   문제가 해결되었으며 문자를 삭제하거나 맞춤법 오류를 지정하지 않습니다.
* Zendesk#31485 - DrmManager in 2.5

   새 DrmManager(컨텍스트 컨텍스트 컨텍스트)를 통해 DrmManager 만들기에서 문제가 발생했습니다. DRMManager를 제공하는 DRMService 클래스를 구현했습니다.
* Android에서 재생되지 않는 Zendesk#32794- 1080P 해상도 스트림

   프레임 높이 및 프레임 너비를 반환하는 데 사용되는 2.5에서 SizeAvailableEvent 및 Previous, getHeight() 및 getWidth() 메서드를 변경했는데, 이 메서드는 미디어 형식으로 반환됩니다. 이제 디코더에서 반환된 출력 높이 및 출력 너비를 각각 반환합니다.
* 세트 수준 매니페스트에서 #EXT-X-FAXS-CM 특성의 위치로 인해 Zendesk #19359 Flash Player가 충돌합니다.

   개별 비트 전송률이나 세그먼트가 재생 목록에 표시되기 전에 #EXT-X-FAXS-CM 태그가 항상 맨 위 재생 목록에 나타나야 합니다.

**Android TVSDK 2.5.2**

* Zendesk#17305 비불투명 배경의 닫힌 캡션의 결함

   TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* Zendesk#25097 CC 디스플레이에는 CC 설정이 있는 시각적 결함이 있습니다.

   TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* Zendesk #31620 TVSDK 플레이어에서 나가는 사용자 에이전트 문자열이 잘립니다.

   사용자 에이전트 문자열은 128자 이후에 잘리지 않습니다.

   Adobe Primetime 버전 문자열이 시스템 사용자 에이전트에 추가됩니다.

* Zendesk #30809 SEEK_END 누락 이벤트는 앱이 재생 상태로 전환되지 않도록 합니다.
* Zendesk #30415 Closed Caption의 &#39;Cyan&#39; 색상은 이전 Primetime TVSDK 릴리스와 비교하여 더 어두운 파란색(터키색)으로 바뀌었습니다.

   색상이 DarkCyan에서 Cyan으로 변경됩니다.

* Zendesk #30727 VOD 광고가 다운로드/해결되고 있지 않습니다.

   VMAP XML에서 명확한 닫기 태그(&#39;&lt;/VAST>&#39;)가 없고 줄바꿈 문자가 없는 빈 VAST 태그가 있으면 VMAP XML이 제대로 구문 분석되지 않고 광고가 재생되지 않을 수 있습니다.

**Android TVSDK 2.5.1**

* 장치별(삼성 갤럭시 탭 4) 충돌;Auditude를 사용하여 VOD DRM LBA를 실행하고 광고를 클릭합니다.
* VHL - 옵셋에서 컨텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생되면 event:type:play 광고에 대한 VHL 하트비트 호출이 누락됩니다.
* COMPLETE 상태로 전환하면 플레이어는 포스트롤 광고에 대한 SKIP adBreakPolicy와 함께 PLAYING 상태로 돌아갑니다.
* 나가는 광고 콜백에 쿠키가 첨부되지 않습니다.
* 광고 큐 포인트는 표시되지 않습니다.
* 별도의 EAC3 SAP 트랙이 있는 HLS가 로드되지 않습니다.
* 미디어 플레이어를 복원한 후 TVSDK에서 의도한 대로 화면을 받을 때 플레이어가 충돌합니다.

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

* CMAF(CBC) 스트림에 대한 ID3, 자막, 지연 바인딩 오디오 지원이 확인되지 않았습니다.
* 일부 장치에서는 CMAF 스트림에서 트릭 재생 중에 맨 위에 비디오 왜곡이 나타날 수 있으므로 재생성이 낮은 문제가 발생합니다.

**Android TVSDK 3.3**

* clcp:c608 캡션은 CMAF 스트림 재생에 대해 지원되지 않습니다.

**Android TVSDK 3.2**

* TVSDK 3.2는 CMAF 샘플 AES 및 AES128 스트림 재생을 지원하지 않습니다.
* HEVC CMAF 스트림에는 자막 재생에 대한 지원이 포함되어 있지 않습니다.
* 암호화되지 않은 세그먼트 주변에서 검색을 수행할 때 WV 암호화된 스트림에 대해 녹색 색상이 표시됩니다.
* CMAF 스트림은 ID3 이벤트를 지원하지 않습니다.
* HLS 스트림은 HTML 캡션 형식을 지원하지 않습니다.

**Android TVSDK 3.0**

* 이 릴리스에서는 HEVC 지원에 다음과 같은 제한 사항이 있습니다.

   * DRM이 지원되지 않음
   * CC(CEA 608/708) 지원이 확인되지 않음
   * 4K 지원이 아직 제공되지 않음
   * ID3 태그 지원이 확인되지 않음

* 광고 진행 이벤트의 경우 타임라인 막대가 100% 정확한 광고 재생 시간을 반영하지 못할 수 있습니다. 이에 대한 해결 방법으로, 사용자는 광고 재생 완료를 알고 타임라인 표시줄 업데이트, 광고 관련 UI 제거 등과 같은 다양한 용도로 UI를 업데이트할 `adcompleteevent` 수 있습니다.
* VMAP에서 반환되는 방대한 광고 호출은 적시 예측 위치를 준수하지 않습니다.

**Android TVSDK 2.5.6**

* 동시에 여러 VMAP 광고 중단은 지원되지 않습니다.

**Android TVSDK 2.5.3**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생은 저가의 장치에서 오디오-비디오 동기화 문제가 있거나 네트워크 상태가 좋지 않을 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.
* 지연 바인딩 오디오 내용을 검색할 때 재생이 중단될 수 있습니다.
* 간헐적으로, LIVE 컨텐츠에 대한 webVTT 캡션이 동기화되지 않을 수 있습니다.
* 간헐적으로, 광고 중단 후 몇 개의 프레임을 빠르게 재생할 수 있습니다.
* Ads가 재생되더라도 Tripple Wrapper 광고 브레이크에 대해 303 오류가 발생하는 경우가 있습니다.

**Android TVSDK 2.5.2**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에 저해상도 장치에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* VOD 미디어 끝을 검색할 때 재생이 간혹 중단될 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.

**Android TVSDK 2.5.1**

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생 시 저해상도 장치에서 오디오-비디오 동기화 문제가 발생할 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.
* VMAP XML에서 명시적 닫기 태그(&lt;/VAST>)가 없는 빈 VAST 태그가 있고 그 뒤에 새 줄이 없으면 VMAP XML이 제대로 구문 분석되지 않으며 광고가 재생되지 않을 수 있습니다.
* VPAID 포스트롤은 지원되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* [시스템 요구 사항](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [Android용 TVSDK 3.10 프로그래머 가이드](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API 문서](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - 각 Java 클래스에는 해당 C++ 클래스가 있으며 C++ 설명서에는 Javadocs보다 더 많은 설명서가 포함되어 있습니다. 따라서 Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.
* [Android(Java)용 TVSDK 1.4-2.5 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 화면 켜기/끄기 시나리오를 처리하려면 빌드에 포함된 `Application_Changes_for_Screen_On_Off.pdf` 파일을 참조하십시오.
* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.
