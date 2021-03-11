---
title: Android용 TVSDK 2.7 릴리스 정보
description: Android용 TVSDK 2.7 릴리스 정보에서는 TVSDK Android 2.7의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '4095'
ht-degree: 0%

---


# Android용 TVSDK 2.7 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 2.7 릴리스 정보에서는 TVSDK Android 2.7의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다

## TVSDK Android 2.7 {#tvsdk-android}

Android 참조 플레이어는 배포 샘플/디렉토리에 Android TVSDK에 포함되어 있습니다. 함께 제공되는 README&lt;.md 파일은 참조 플레이어를 구축하는 방법을 설명합니다.

>[!NOTE]
>
>릴리스와 함께 배포된 README.md에 설명된 대로 참조 플레이어를 성공적으로 구축하려면 다음을 수행하십시오.
>
>1. [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)에서 VideoHeartbeat.jar 다운로드(Android v2.0.0용 VideoHeartbeat 라이브러리)
>1. VideoHeartbeat.jar를 libs/ 폴더에 추출합니다.

>



## 새 기능 {#new-features}

Android용 TVSDK 2.7에는 [Feature Matrix](#feature-matrix) 아래에 나열되지 않은 기능을 제외한 버전 1.4의 모든 기능이 포함되어 있습니다.

**Android TVSDK 2.7**

* **병렬 광고 해상도 지원**

TVSDK 2.7은 순차적 해상도가 아니라 광고 브레이크에서 모든 광고 요청의 동시 해결을 지원합니다.

### 이전 릴리스의 새로운 기능 {#new-features-previous-releases}

**버전 2.5.6**

* **TVSDK 2.5는 Android P 지원**
* **백그라운드 오디오 활성화**

   앱이 전경 상태에서 배경으로 이동할 때 오디오 재생을 활성화하려면 플레이어가 준비 상태일 때 MediaPlayer의 enableAudioPlaybackInBackground API를 인수로 호출해야 합니다.

* **MediaPlayer 클래스의 alwaysUseAudioOutputLatency(boolean val)**

설정할 때 오디오 타임스탬프 계산에서 출력 지연을 사용합니다.
부울 매개 변수 val - True는 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

* **대역폭 속도가 갑자기 끊기는 경우에도 최고의 재생 경험을 제공하도록 최적화되었습니다.**
이제 TVSDK가 필요한 경우 진행 중인 세그먼트 다운로드를 취소하고 적절한 변환으로 동적으로 전환합니다. 중단 없이 비트 전송률을 원활하게 전환하여 수행할 수 있습니다.

**버전 2.5.5**

* **부분 광고 분리 삽입**

   부분적으로 시청한 광고에 대한 추적을 시작하지 않고 광고 중간에 참여하는 TV와 같은 경험.\
   예**:**사용자는 3개의 30초 광고로 구성된 90초 광고 중단의 중간(40초)에 참여합니다. 이것은 10초 동안 2차 광고 뒤에 있습니다.
   * 나머지 기간(20초) 동안 두 번째 광고가 재생되고 세 번째 광고가 재생됩니다.
   * 부분 재생(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기가 실행됩니다.

* **HTTPS를 통한 안전한 광고 로딩**

   Adobe Primetime은 https를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

* **AdSystem 및 Creative Id가 CRS 요청에 추가됨**

   * 이제 1401 및 1403 요청에서 새 매개 변수로 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 포함합니다.

* **NetworkConfiguration 클래스의 API setEncodeUrlForTracking은 URL에서 안전하지 않은 문자** 를 인코딩해야 합니다.

**버전 2.5.4**

Android TVSDK v2.5.4은 다음 업데이트 및 API 변경 사항을 제공합니다.

* WebViewDebuging에 대한 기본값 변경
WebViewDebuging 값은 기본적으로 False로 설정됩니다. 이를 활성화하려면 응용 프로그램에서 setWebContentsDebuggingEnabled(true)를 호출합니다.
* OpenSSL 및 Curl 버전 업그레이드
v7.57.0 및 OpenSSL로 libcurl을 v1.0.2k로 업데이트했습니다.
* VAST 응답 개체에 대한 앱 수준 액세스
응용 프로그램에 대한 VAST 응답 객체에 대한 액세스를 제공하는 새로운 API NetworkAdInfo::getVastXml()이 도입되었습니다.

**버전 2.5.3**

Android TVSDK v2.5.3은 다음 업데이트 및 API 변경 사항을 제공합니다.

* CRS를 사용하는 모든 TVSDK 고객은 TVSDK 2.5.3.85 또는 최신 버전의 Android로 앱을 업그레이드할 수 있습니다. 기존 앱 구현이 드롭인 대신 사용됩니다. TVSDK 업그레이드 후 프록시 도구에서 CRS 크리에이티브 URL 요청을 확인합니다(예:Charles)를 클릭하고 경로의 호스트 이름과 버전이 아래 샘플 URL 구조와 같이 반영되는지 확인합니다.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK의 사용자 에이전트 사용자 지정 가능:사용자 에이전트를 사용자 정의하기 위한 일부 새로운 API를 추가했습니다.

   * setCustomUserAgent(문자열 값)
   * getCustomUserAgent()

* Android Application 및 TVSDK 간 쿠키 공유:Android TVSDK는 이제 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간의 쿠키 액세스를 지원합니다. 이제 Java 쿠키 저장소에 노출되므로 기본 C++ 레이어에서 쿠키를 설정하고/또는 수정할 수 있습니다.
* API 변경 사항:

   * 새 이벤트 쿠키 UpdatedEvent가 추가됩니다. 쿠키가 업데이트되면 미디어 플레이어에 의해 전달됩니다.
   * 사용자 지정 사용자 에이전트를 사용하기 위해 새 API가 NetworkConfiguration::set/ getCustomUserAgent()에 추가됩니다.
   * 안전하지 않은 문자 인코딩을 강제 적용하려면 NetworkConfiguration::set/ getEncodedUrlForTracking에 새 API가 추가됩니다.
   * 장애 조치(failover)의 경우 네트워크 확인 URL을 설정하기 위해 새 API가 NetworkConfiguration::getNetworkDownVerificationUrl()에 추가됩니다.
   * 캡션을 표시할 때 공간을 영숫자로 처리할지 여부를 정의하는 TextFormat::treatSpaceAsAlphaNum에 새 속성이 추가됩니다.

* SizeAvailableEvent의 변경 사항:이전에는 미디어 형식으로 반환된 프레임 높이 및 프레임 폭을 반환하는 데 사용되는 2.5.2의 SizeAvailableEvent의 getHeight() 및 getWidth() 메서드가 미디어 형식으로 반환되었습니다. 이제 디코더에서 각각 반환된 출력 높이 및 출력 너비를 반환합니다.
* 버퍼링 동작의 변경 사항:버퍼링 동작이 변경되었습니다. 버퍼가 비어 있는 경우 원하는 작업을 앱 개발자에게 맡겼다. 2.5.3 버퍼 빈 상황에서 재생 버퍼 크기를 사용합니다.

**버전 2.5.2**

Android TVSDK v2.5.2은 중요한 버그 수정과 몇 가지 API 변경 사항을 제공합니다.

**버전 2.5.1**

Android 2.5.1에서 릴리스된 중요한 새로운 기능입니다.

* **성능**&#x200B;개선 새로운 TV SDK 2.5.1 아키텍처는 많은 성능 향상을 가져옵니다. 제3자 벤치마크 조사 결과에 따르면 새로운 아키텍처는 업계 평균에 비해 시작 시간이 5배 단축되고 드롭된 프레임이 3.8배 감소하여 시작 시간을 단축합니다.

   * **VOD 및 실시간** 을 위한 인스턴트 온 - 인스턴트 온 기능을 활성화하면 재생이 시작되기 전에 TVSDK가 초기화되고 미디어를 버퍼링합니다. 백그라운드에서 여러 MediaPlayerItemLoader 인스턴스를 동시에 실행할 수 있으므로 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 재생이 즉시 시작됩니다. 또한 TVSDK 2.5.1은 **live** 스트림에 대해 인스턴트 온을 지원합니다. 라이브 윈도우를 이동하면 라이브 스트림이 다시 버퍼링됩니다.

      * **향상된 ABR 논리 -** 새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 속도 및 측정된 대역폭을 기반으로 합니다. 따라서 ABR은 대역폭이 변경될 때 올바른 비트 전송률을 선택하고 버퍼 길이가 변경되는 속도를 모니터링하여 비트율 스위치가 실제로 발생하는 횟수를 최적화합니다.
      * **부분 세그먼트 다운로드/하위 세그먼트 -** TVSDK는 가능한 한 빨리 재생을 시작할 수 있도록 각 조각의 크기를 추가로 줄입니다. 조각에는 2초마다 키 프레임이 있어야 합니다.
      * **게으른 광고 해상도 -** TVSDK는 재생을 시작하기 전에 비프리롤 광고의 해상도를 기다리지 않으므로 시작 시간을 줄일 수 있습니다. 검색 및 트릭 플레이와 같은 API는 모든 광고가 해결될 때까지 사용할 수 없습니다. 이것은 CSAI와 함께 사용되는 VOD 스트림에 적용됩니다. 검색 및 빨리 감기 등의 작업은 광고 해상도가 완료될 때까지 허용되지 않습니다. 실시간 스트림의 경우 라이브 이벤트 중에는 광고 해상도에 대해 이 기능을 활성화할 수 없습니다.
      * **영구 네트워크 연결 -** 이 기능을 통해 TV SDK는 영구 네트워크 연결의 내부 목록을 만들고 저장할 수 있습니다. 이러한 연결은 각 네트워크 요청에 대해 새 연결을 열고 나중에 삭제하는 대신 여러 요청에 대해 다시 사용됩니다. 이렇게 하면 네트워킹 코드의 효율성이 높아지고 지연이 줄어들어 재생 성능이 빨라집니다.
TVSDK가 연결을 열면 서버에 *keep-alive* 연결을 요청합니다. 일부 서버는 이러한 유형의 연결을 지원하지 않을 수 있습니다. 이 경우 TVSDK는 각 요청에 대해 다시 연결을 수행하는 것으로 돌아갑니다. 또한 지속적인 연결은 기본적으로 켜져 있지만 TVSDK에는 앱이 원하는 경우 영구 연결을 해제할 수 있는 구성 옵션이 있습니다.
      * **병렬 다운로드 -** 비디오 및 오디오를 시리즈가 아닌 동시에 다운로드할 경우 시작 지연이 줄어듭니다. 이 기능을 사용하면 HLS Live 및 VOD 파일을 재생할 수 있고, 서버의 사용 가능한 대역폭 사용을 최적화하며, 버퍼가 실행되기 전에 발생할 가능성이 낮아지며, 다운로드와 재생 간의 지연을 최소화합니다.
      * **병렬 광고 다운로드 -** TVSDK는 광고를 중단하기 전에 컨텐츠 재생과 동시에 광고를 프리페치하므로 광고와 컨텐츠를 매끄럽게 재생할 수 있습니다.

* **재생**

   * **MP4 컨텐츠 재생 -** MP4 짧은 클립을 TVSDK 내에서 재생하기 위해 다시 코딩할 필요가 없습니다.
참고:MP4 재생에는 ABR 전환, 트릭 재생, 광고 삽입, 지연 오디오 바인딩 및 하위 세그멘테이션이 지원되지 않습니다.
   * **ABR(Trick play with adaptive bit rate) -** 이 기능을 사용하면 TVSDK가 트릭 재생 모드에서 iFrame 스트림 간을 전환할 수 있습니다. iFrame이 아닌 프로파일을 사용하여 보다 빠른 속도로 trick play를 할 수 있습니다.
   * **보다 매끄러운 트릭 재생 -** 이러한 향상된 기능을 통해 사용자 경험을 향상시킬 수 있습니다.

          * 트릭 재생 중에 대역폭 및 버퍼 프로파일
           기반의 적응 비트 전송률과 프레임 속도 선택* IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps의 빠른 재생을 수행할 수 있습니다.
      
* **컨텐츠 보호**

   * **해상도 기반 출력 보호 -** 이 기능은 재생 제한을 특정 해상도에 연결하여 보다 세밀하게 그래프로 배치된 DRM 컨트롤을 제공합니다.

* **워크플로우 지원**

   * **직접 청구 통합 -** 이 대금 청구 지표를 Adobe Analytics 백엔드로 보냅니다. 이 백엔드는 고객이 사용하는 스트림에 대해 Adobe Primetime에서 인증합니다.
TVSDK는 고객 판매 계약을 준수하여 청구 목적에 필요한 정기적인 사용 보고서를 자동으로 수집합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림의 지속 시간을 기반으로 콘텐츠 유형, 광고 삽입 활성화 플래그 및 DRM 지원 플래그와 같은 청구 측정 단위를 Adobe Analytics Primetime 소유 보고서 세트로 전송합니다. 이것은 고객의 자체 Adobe Analytics 보고서 세트 또는 서버 호출에 간섭하거나 포함되지 않습니다. 요청 시 이 청구 사용량 보고서는 고객에게 정기적으로 전송됩니다. 청구 기능이 사용 과금만을 지원하는 첫 번째 단계입니다. 설명서에 설명된 API를 사용하여 판매 계약에 따라 구성할 수 있습니다. 이 기능은 기본적으로 활성화되어 있습니다. 이 기능을 끄려면 참조 플레이어 샘플을 참조하십시오.
   * **향상된 장애 조치 지원 -** 호스트 서버, 재생 목록 파일 및 세그먼트에 장애가 발생하더라도 중단 없이 계속 재생할 수 있도록 구현된 추가 전략입니다.

* **광고**

   * **해자 통합 -해자에서** 광고 보기 측정을 지원합니다.
   * **컴패니언 배너 -** Companion 배너는 선형 광고와 함께 표시되며 광고가 종료된 후에도 종종 보기에 계속 표시됩니다. 이러한 배너는 html(HTML 조각) 유형이거나 iframe(iframe 페이지에 대한 URL)을 입력할 수 있습니다.

* **분석**

   * **VHL 2.0 -** Adobe Analytics에 대한 사용 데이터 자동 수집을 위해 최적화된 최신 VHL(Video Heartbeats Library) 통합입니다. 구현을 용이하게 하기 위해 API의 복잡성을 줄였습니다. Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)용 VHL 라이브러리 [v2.0.0을 다운로드하고 libs 폴더에 JAR 파일을 추출합니다.

* **SizeAvalableEventListener**
   * 이제 SizeAvailableEvent의 getHeight() 및 getWidth() 메서드가 각각 높이와 폭으로 출력을 반환합니다. 디스플레이 종횡비는 다음과 같이 계산할 수 있습니다.

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **쿠키**

   * Android TVSDK는 이제 Android 애플리케이션의 CookieStore에 저장된 JAVA 쿠키에 대한 액세스를 지원합니다. 새 쿠키가 &quot;Set-Cookie&quot; 응답 헤더의 일부로 들어올 때마다 레코딩하기 위해 콜백 API(onCookiesUpdated)가 제공됩니다. 이러한 쿠키는 CookieStore를 사용하여 특정 URI/도메인에 이러한 쿠키 값을 설정하여 다른 URI/도메인에 사용되는 HttpCookie 목록 형태로 사용할 수 있습니다. 마찬가지로 TVSDK의 쿠키 값은 CookieStore 추가 API를 사용하여 업데이트됩니다.

## 기능 매트릭스 {#feature-matrix}

Android용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

아래 기능 표에서 &#39;Y&#39;는 이 기능이 현재 릴리스에서 지원됨을 나타냅니다.

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생(재생, 일시 정지, 검색) | VOD + 라이브 | Y |
| FER - 일반 재생(재생, 일시 중지, 검색) | FER VOD | Y |
| 광고 재생 시 검색 | VOD + 라이브 | 지원되지 않음 |
| AC3 | VOD + 라이브 | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 |
| MP4 내용 재생 | VOD | Y |
| 적응형 비트 전송률 전환 논리 | VOD + 라이브 | Y |
| 오디오 전용 재생 | VOD + 라이브 | Y |
| 다중 CDN 지원 | VOD + 라이브 | 지원되지 않음 |
| 오디오 전용 미디어를 사용한 광고 재생 | VOD + 라이브 | 지원되지 않음 |
| 자막 - 608/708 | VOD + 라이브 | Y |
| 자막 - WebVTT | VOD + 라이브 | Y |
| 매니페스트 장애 조치(failover) | VOD + 라이브 | Y |
| 고급 페일오버 | VOD + 라이브 | Y |
| QoS 및 플레이어 알림 | VOD + 라이브 | Y |
| 쿠키 헤더 지원 | VOD + 라이브 | Y |
| 사용자 정의 HTTP 헤더 지원 | VOD + 라이브 | Y(목록 허용 필수) |
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
| 광고 일시 중단 | VOD + 라이브 | 지원되지 않음 |
| 즉시 켜기 | VOD + 라이브 | 지원되지 않음 |
| 비연속성 마커 지원 | VOD + 라이브 | Y |
| 302 리디렉션 지속 | VOD + 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생, 광고 활성화 | VOD + 라이브 | Y |
| 광고가 활성화된 FER 컨텐츠 | VOD | Y |
| 기본 광고 비헤이비어 | VOD + 라이브 | Y |
| VAST 2.0/3.0 | VOD + 라이브 | Y |
| VMAP 1.0 | VOD + 라이브 | Y |
| MP4 광고 | VOD + 라이브 | Y(CRS에서) |
| 광고를 사용하여 트릭 플레이 사용 | VOD + 라이브 | Y |
| 광고 전용 | VOD | Y |
| 타깃팅 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 매개 변수 | VOD + 라이브 | Y |
| 사용자 지정 광고 비헤이비어 | VOD + 라이브 | Y |
| 사용자 지정 광고 태그 | 라이브 | Y |
| 사용자 지정 광고 해상도 | VOD + 라이브 | Y |
| 자유 바퀴 사용자 지정 광고 확인자 | VOD | Y |
| C3 | VOD + 라이브 | 지원되지 않음 |
| 레이지 광고 해결 | VOD | Y |
| 불연속성 마커 지원 - SSAI | VOD + 라이브 | Y |
| 부록 광고, 배너 광고 및 클릭 가능한 광고 | VOD + 라이브 | Y |
| VPAID 2.0 | VOD + 라이브 | Y(JS) |
| 조기 광고 종료 | 라이브 | Y |
| 규칙 기반의 크리에이티브 우선 순위 | VOD + 라이브 | Y |
| CRS 규칙 | VOD + 라이브 | Y |
| JSON 광고 확인자 | VOD + 라이브 | 지원되지 않음 |
| 해자 통합 | VOD + 라이브 | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| AES 암호화 | VOD + 라이브 | Y |
| 샘플 AES 암호화 | VOD + 라이브 | Y |
| 토큰화된 스트림 | VOD + 라이브 | Y |
| DRM | VOD + 라이브 | Primetime DRM만 해당(향후:Widevin) |
| 외부 재생(RBOP) | VOD + 라이브 | Primetime DRM만 해당 |
| 라이선스 순환 | VOD + 라이브 | Primetime DRM만 해당 |
| 키 회전 | VOD + 라이브 | Primetime DRM만 해당 |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| Adobe Analytics VHL 통합 | VOD + 라이브 | Y |
| 청구 | VOD + 라이브 | Y |

## 해결된 문제 {#resolved-issues}

해상도가 보고된 문제와 연결된 경우 ZD#xxxxx와 같은 Zendesk 참조가 표시됩니다.

**Android TVSDK 2.7**

이 섹션에서는 TVSDK 2.7 릴리스에서 해결된 문제에 대한 요약을 제공합니다.

* ZD#37166 - 광고가 잘 재생될 때에도 오류 추적 호출이 실행됩니다.
* ZD#37134 - VMAP 응답에서 wrapper(3P) 광고에 여러 광고가 있는 경우 잘못된 광고 ID가 반환됩니다.

**Android TVSDK 2.5.6**

* ZD #34992 - 닫힌 캡션에서 언어가 비어 있습니다.
   * TVSDK가 캡션 추적 세부 정보를 가져오기 위해 기본 매니페스트에서 #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS를 구문 분석하지 않는 문제가 해결되었습니다.
* ZD #35078 - Android P 유효성 검사.
   * TVSDK 2.5.6은 최신 Android P 베타 빌드를 통해 유효성이 검증되었습니다. 새로운 Android OS로 인해 발견된 문제가 없습니다.
* ZD #34149 - 오류가 발생하더라도 플레이어가 매니페스트를 계속 요청합니다.
   * 모든 프로필이 다운된 경우에도(404 오류) TVSDK에서 반복적인 호출을 하던 문제가 수정되었습니다.
* ZD #31533 - 앱이 백그라운드로 전송되는 후 Android에서 오디오를 재생합니다.
   * 앱이 백그라운드에 있을 때 오디오를 재생할 수 있도록 &#39;True&#39;로 호출해야 하는 MediaPlayer의 `enableAudioPlaybackInBackground` API를 추가했습니다(플레이어가 준비 상태일 때).

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK는 실제 비디오 크기가 640x360이면 640x368로 알립니다.
   * 변수 m_nOutputHeight(AndroidMCVideoDecoder 내)가 실제 출력 높이 대신 프레임 높이로 업데이트되기 때문입니다. getVideoFrame 함수에서 m_nOutputHeight를 올바르게 계산하도록 관련 변경 작업을 수행했습니다.
* ZD #26614 - Emergency — 타사 광고 서비스/프로그래머틱 광고 — 노출 횟수 실패
   * &quot;space&quot;가 &lt;VAST 버전 =&quot;2.0&quot;> 등과 같이 &quot;equal&quot; 기호 앞에 있을 때 문제가 재현될 때 XML 구문 분석에서 문제를 처리하여 이전 수정 사항을 개선했습니다.
* ZD #29296 - Android:CRS 요청에 AdSystem 및 Creative ID를 추가합니다.
   * 이제 1401 및 1403 요청에서 새 매개 변수로 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 포함합니다.
* ZD #33062 - CDATA 노드 아래의 VAST 응답에서 파이프 문자가 발생할 때 TVSDK 충돌 발생
   * NetworkConfiguration 클래스의 API setEncodeUrlForTracking은 인코딩할 URL의 안전하지 않은 문자로 제거되었습니다.
* ZD #33063 - CRS 파일 선택 로직이 손상되었습니다. - TVSDK가 웹 m 포맷에 대한 CRS 요청을 전송하지 않고 대신 3gpp 파일에 대해 CRS 요청을 전송했습니다.
   * 이제 논리를 수정했습니다. webm 및 3gpp 형식의 미디어 파일을 사용하는 경우 CRS 요청을 웹에 보낼 수 있습니다. 또한 3gpp 형식의 미디어 파일을 모두 사용할 경우 최고 비트 전송률 3gpp 파일에 대해 CRS 요청을 전송합니다.
* ZD #33125 - Android 앱이 VMAP 내의 특정 DoubleClick 태그와 충돌합니다.
   * 충돌을 방지하기 위해 시나리오를 수정했습니다.
* ZD #32256 - 라이선스 순환 및 키 순환 문제 - Adobe 액세스.
   * SampleAES 컨텐츠에 대한 DRM 메타데이터로 세그먼트 초기화를 수정했습니다. AES128 컨텐츠와 잘 작동합니다.
* ZD #33619 - 라이브 지점 근처의 버퍼링 상태에 있는 증가하는 재생 목록 내용을 빠르게 전달합니다.
   * 트릭 재생 모드에서 라이브 포인트를 지날 때 이 문제를 처리했습니다.
* ZD #34151 - TimedMetadata 개체의 순서가 잘못되었습니다.
   * 타임라인에서 동일한 시간에 속하는 두 개의 TimedMetadata 이벤트가 임의의 순서로 표시되었습니다. 원래 순서를 분명히 유지합니다.
* ZD #34189 - 광고 분리를 시작할 때 발생하는 문제입니다.
   * 그 문제는 불연속성을 사용하여 봉합된 SSSAI 광고에서 있었다. 그 원인은 우리가 그러한 광고의 시작 부분을 찾고자 할 때, 키프레임을 찾지만 찾지 못하는 행동이었습니다. 최소 비디오 타임스탬프 이전에 광고의 최소 오디오 타임스탬프가 있었던 이유입니다. 따라서 잘못된 fragmentDump 데이터에서 키 프레임을 검색합니다. 수정했습니다.
* ZD #34528 - FireTV 3세대 동글 기반의 비디오 해상도가 640x360을 초과하지 않습니다.
   * 최신 펌웨어 업데이트를 포함하도록 수정 사항을 개선했습니다.
* ZD #34793 - TVSDK 2.5.x가 사용자 지정 컨텐츠 확인자와 충돌하던 경우가 있었습니다. 경우에 따라 VideoEngine은 auditudeSettings를 사용할 수 있고 그렇지 않았다고 가정합니다.
   * Null 공유 포인터(auditudeSettings)에 대한 함수 호출로 인해 충돌이 발생했습니다. VideoEngineTimeline::placeToSourceTimeline() 내에 조건부 검사를 추가하여 auditudeSettings가 해당 객체에 대해 호출하기 전에 사용할 수 있는지 확인합니다.
* ZD #32584 - VAST 응답의 &lt;Extensions> 노드에 있는 전체 정보에 액세스할 수 없습니다.
   * XML 구문 분석 문제를 해결했으며 NetworkAdInfo가 &lt;Extensions> 노드에 있는 전체 정보를 제공합니다.
* ZD #35086 - 특정 VMAP 응답의 경우 플레이어에서 전체 확장 데이터를 가져올 수 없습니다.
   * 확장 xml에 특성 값 내에 큰 따옴표가 있는 경우 XML 구문 분석이 작동하지 않으므로 확장 xml에 문제가 있었습니다. 문제를 수정했습니다.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - 웹 뷰 원격 디버깅을 사용하는 재생 세션입니다.
   * WebViewDebuging은 기본적으로 False로 설정됩니다. 디버깅을 활성화하려면 setWebContentsDebuggingEnabled(true)를 사용하여 응용 프로그램을 통해 true로 설정합니다.
* ZenDesk#33011 - CRS 요청이 실패한 경우 광고 타임라인이 확인되지 않습니다.
   * 광고에 대한 CRS 요청이 실패하면 타임라인이 해결되고 나머지 광고가 재생됩니다.
* ZenDesk#34528 - 비디오 해상도는 FireTV 3세대 동글 640x360을 넘어서까지 업그레이드되지 않습니다.
   * 비디오 해상도는 비트 전송률 스위치로 전환됩니다.
* ZenDesk#33192 - AudioUpdatedEventListener::onAudioUpdated를 통해 트랙을 검색할 때 AudioTrack에 null 이름이 있습니다.
   * FireTV Stick에 대한 몇 가지 시나리오에서 실제 오디오 업데이트가 없을 때 onAudioUpdate 이벤트가 실행되었습니다. 이제 수정되었습니다.

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata 사용자 지정 태그 구독이 작동하지 않습니다.
   * ID3 데이터를 바이트 배열로 반환(APIC 또는 범용 데이터 지원)하는 반면 1.4 반환 문자열은 클라이언트로 반환됩니다. 바이트 배열은 null 종료 문자 자체를 처리하지 않으므로 클라이언트에 특수 문자를 표시했습니다. 이제 이 문제가 해결되었습니다.
* Zendesk#32670 - 플레이어가 중복 재생 목록으로 장애 없음
   * 이 작업은 이제 제대로 작동하므로 setNetworkDownVerificationUrl이 예상대로 작동합니다.
* Zendesk#32369 - 닫힌 캡션은 다른 색상 가비지 또는 가공물을 표시합니다.
   * 최신 빌드에서 CC 문제 해결
* Zendesk#25590 - 개선:TVSDK 쿠키 저장소(C++에서 JAVA로)
   * Android TVSDK는 이제 JAVA 레이어(Android 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간의 쿠키 액세스를 지원합니다.
* Zendesk#32252 - TVSDK_Android_2.5.2.12은 PTPLAY-20269에 대한 수정 사항이 없는 것 같습니다.
이 문제는 수정되었으며 2.5.2 분기에 통합되었습니다.
* Zendesk#31806 - 준비 중인 Auditude 막대
응답 xml에 빈 태그가 있기 때문에 플레이어가 준비 중 상태로 정지되었습니다. 이제 문제가 해결되었습니다.
* Zendesk#31727 - TVSDK 2.5 자막 문자가 누락되거나 맞춤법이 틀린 경우
   * 문제가 해결되었으며 문자를 가져오거나 맞춤법 오류를 지정하지 않습니다.
* Zendesk#31485 - DrmManager in 2.5
   * 새 DrmManager(컨텍스트 컨텍스트)를 통해 DrmManager 만들기에 문제가 발생했습니다. DRMManager를 제공하는 DRMService 클래스를 구현했습니다.
* Android에서 재생되지 않는 Zendesk#32794-1080P 해상도 스트림입니다.
   * 미디어 형식으로 반환된 프레임 높이 및 프레임 폭을 반환하는 데 사용되는 2.5에서 SizeAvailableEvent 및 Previous, getHeight() 및 getWidth() 메서드를 변경했습니다. 이제 디코더에서 각각 반환된 출력 높이 및 출력 너비를 반환합니다.
* 세트 수준 매니페스트의 #EXT-X-FAXS-CM 특성 위치로 인해 Zendesk #19359 Flash Player이 충돌합니다.
   * #EXT-X-FAXS-CM 태그는 개별 비트 전송률이나 세그먼트가 재생 목록에 표시되기 전에 항상 맨 위 재생 목록에 나타나야 합니다.

**Android TVSDK 2.5.2**

* Zendesk#17305 비불투명 배경의 닫힌 캡션에 가공물이 있습니다.
TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* Zendesk#25097 CC 디스플레이에는 CC 설정이 있는 시각적 가공물이 있습니다.
TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* TVSDK 플레이어에서 나가는 Zendesk #31620 사용자 에이전트 문자열이 잘립니다.
사용자 에이전트 문자열은 128자 이후에 잘리지 않습니다.
Adobe Primetime 버전 문자열이 시스템 사용자 에이전트에 추가됩니다.

* Zendesk #30809 Missing SEEK_END 이벤트는 앱이 재생 상태로 전환되지 않도록 합니다.
* 이전 Primetime TV SDK 버전과 비교하여 Zendesk #30415 Closed Caption의 &#39;Cyan&#39; 색상이 이제 더 어두운 파란색(터키색)으로 바뀌었습니다.

   색상이 DarkCyan에서 Cyan으로 변경됩니다.

* Zendesk #30727 VOD 광고가 다운로드/해결되고 있지 않습니다.

   VMAP XML에서 명확한 닫기 태그(&#39;&lt;/VAST>&#39;)가 없고 줄바꿈 문자가 없는 빈 VAST 태그가 있으면 VMAP XML이 제대로 구문 분석되지 않으며 광고가 재생되지 않을 수 있습니다.

**Android TVSDK 2.5.1**

* 장치별(Samsung Galaxy Tab 4) 충돌;Auditude를 사용하여 VOD DRM LBA를 실행하고 광고를 클릭합니다.
* VHL - 오프셋에서 컨텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생되면 event:type:play 광고에 대한 VHL 하트비트 호출이 누락됩니다.
* COMPLETE 상태로 전환하면 플레이어는 포스트롤 광고에 대해 SKIP adBreakPolicy가 있는 PLAYING 상태로 돌아갑니다.
* 나가는 광고 콜백에 쿠키가 첨부되지 않습니다.
* 광고 큐 포인트가 표시되지 않습니다.
* 별도의 EAC3 SAP 트랙이 있는 HLS는 로드되지 않습니다.
* 미디어 플레이어를 복원한 후 TVSDK에서 의도한 대로 화면을 받을 때 플레이어가 충돌합니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

**Android TVSDK 2.7**

* TVSDK 2.7은 최대 5개의 광고 동시 해상도를 지원합니다.
* VMAP 응답의 경우 단일 광고 나누기의 광고 호출이 동시에 진행되며 광고 할당이 순차적으로 해결됩니다.
* FER의 경우 각 기회의 광고 호출이 동시에 해결됩니다.

### 이전 릴리스의 알려진 문제 및 제한 사항{#known-issues-limitations-previous-releases}

**Android TVSDK 2.5.6**

* 동시에 여러 VMAP 광고 중단은 지원되지 않습니다.

**Android TVSDK 2.5.3**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생은 낮은 최종 장치에서 오디오-비디오 동기화 문제가 있거나 네트워크 상태가 좋지 않을 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime은 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.
* [지연 바인딩 오디오] 내용을 검색할 때 재생이 중단될 수 있습니다.
* 간헐적으로, webVTT 캡션이 라이브 컨텐츠에 대해 동기화되지 않을 수 있습니다.
* 간헐적으로 일부 프레임의 신속한 재생이 광고 중단에서 나온 후에 표시될 수 있습니다.
* Ads가 재생되더라도 Tripple Wrapper 광고 중단에 대해 303 오류가 발생하는 경우가 있습니다.

**Android TVSDK 2.5.2**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생은 저가의 장치에서 오디오-비디오 동기화 문제를 가질 수 있습니다.
* VOD 미디어 끝을 검색할 때 재생이 간혹 지연될 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime은 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.

**Android TVSDK 2.5.1**

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생은 로우 엔드 디바이스에서 오디오-비디오 동기화 문제를 일으킬 수 있습니다.
* FER 스트림의 경우 virtualTime 및 localTime은 다를 수 있습니다. 또한 오프셋이 있는 FER는 작동하지 않습니다.
* VMAP XML에서 명확한 닫기 태그(&lt;/VAST>)가 없는 빈 VAST 태그가 있고 그 뒤에 새 개시가 없으면 VMAP XML이 제대로 구문 분석되지 않으며 광고가 재생되지 않을 수 있습니다.
* VPAID 포스트롤은 지원되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* [시스템 요구 사항](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-requirements.html)
* [Android 프로그래머용 TVSDK 2.7 안내서](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-overview-prod-audience-guide.html)
* [TVSDK Android API용 Javadoc 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android C++ API 문서](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  - 각 Java 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 Javadocs보다 더 많은 설명 자료가 포함되어 있으므로, Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.
* [Android(Java)용 TVSDK 1.4~2.5 마이그레이션 안내서](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 화면 켜기/끄기 시나리오를 처리하려면 빌드에 포함된 `Application_Changes_for_Screen_On_Off.pdf` 파일을 참조하십시오.
* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 설명서를 참조하십시오.