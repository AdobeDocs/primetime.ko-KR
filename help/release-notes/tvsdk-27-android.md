---
title: Android™용 TVSDK 2.7 릴리스 노트
description: Android™용 TVSDK 2.7 릴리스 노트에서는 TVSDK Android™ 2.7의 새로운 기능 또는 변경 사항, 해결되고 알려진 문제 및 장치 문제를 설명합니다
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: d2c8133f126db44b9c505dc0a21ba208fd6c01c8
workflow-type: tm+mt
source-wordcount: '4072'
ht-degree: 0%

---

# Android™용 TVSDK 2.7 릴리스 노트 {#tvsdk-for-android-release-notes}

Android™용 TVSDK 2.7 릴리스 노트에서는 TVSDK Android™ 2.7의 새로운 기능 또는 변경 사항, 해결되고 알려진 문제 및 장치 문제를 설명합니다

## TVSDK Android™ 2.7 {#tvsdk-android}

Android™ 참조 플레이어는 배포의 샘플/디렉토리에 Android™ TVSDK에 포함되어 있습니다. 함께 제공되는 README&lt;.md 파일은 참조 플레이어를 빌드하는 방법을 설명합니다.

>[!NOTE]
>
>릴리스와 함께 배포되는 README.md에 설명된 대로 참조 플레이어를 성공적으로 빌드하려면 다음을 수행하십시오.
>
>1. 에서 VideoHeartbeat.jar 다운로드 [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (Android™ v2.0.0용 VideoHeartbeat 라이브러리)
>1. VideoHeartbeat.jar를 libs/ 폴더에 추출합니다.

>


## 새로운 기능 {#new-features}

Android™용 TVSDK 2.7에는 아래에 나열되지 않은 기능을 제외하고 버전 1.4의 모든 기능이 포함되어 있습니다 [기능 매트릭스](#feature-matrix).

**Android™ TVSDK 2.7**

* **병렬 광고 해상도 지원**

TVSDK 2.7은 순차적 해결 대신 광고 브레이크에서 모든 광고 요청의 동시 해결을 지원합니다.

### 이전 릴리스의 새로운 기능 {#new-features-previous-releases}

**버전 2.5.6**

* **TVSDK 2.5는 Android™ P를 지원합니다.**
* **배경 오디오 활성화**

   앱이 전경 상태에서 백그라운드로 이동할 때 오디오 재생을 활성화하려면 플레이어가 PREPARED 상태일 때 인수가 true인 MediaPlayer의 enableAudioPlaybackInBackground API를 호출해야 합니다.

* **MediaPlayer 클래스의 alwaysUseAudioOutputLatency(부울 값)**

설정할 때 오디오 타임스탬프 계산에서 출력 지연을 사용하십시오.
부울 매개 변수 val - True는 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

* **대역폭 속도가 갑자기 느려지더라도 최적의 재생 경험을 제공하도록 최적화되었습니다.**
이제 TVSDK는 필요한 경우 진행 중인 세그먼트의 다운로드를 취소하고 적절한 표현물로 동적으로 전환합니다. 이 작업은 중단 없이 비트율 간을 원활하게 전환하여 수행됩니다.

**버전 2.5.5**

* **부분 광고 브레이크 삽입**

   부분적으로 시청된 광고에 대한 추적을 실행하지 않고 광고 중간에 참여하는 TV와 같은 경험입니다.\
   예**: **사용자는 3개의 30초 광고로 구성된 90초 광고 브레이크의 중간(40초)에 참여합니다. 브레이크에서 두 번째 광고 10초입니다.
   * 두 번째 광고는 나머지 기간(20초) 동안 재생되고 그 뒤에 세 번째 광고가 재생됩니다.
   * 부분 광고 재생(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기만 실행됩니다.

* **HTTPS를 통해 보안 광고 로드**

   Adobe Primetime은 https를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

* **AdSystem 및 Creative Id가 CRS 요청에 추가되었습니다**

   * 이제 1401 및 1403 요청에 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 새 매개 변수로 포함합니다.

* **NetworkConfiguration 클래스의 API setEncodeUrlForTracking이 제거되었습니다.** URL의 안전하지 않은 문자는 인코딩해야 합니다.

**버전 2.5.4**

Android™ TVSDK v2.5.4는 다음 업데이트 및 API 변경 사항을 제공합니다.

* 에 대한 기본값 변경 `WebViewDebbuging`

   `WebViewDebbuging` 기본적으로 값이 False로 설정됩니다. 이를 활성화하려면 응용 프로그램에서 setWebCon의 tentsDebuggingEnabled(true)를 호출합니다.
* OpenSSL 및 Curl 버전 업그레이드 업데이트됨 `libcurl` v7.57.0 및 OpenSSL을 v1.0.2k로 설정합니다.
* VAST 응답 개체에 대한 앱 수준 액세스 응용 프로그램에 대한 VAST 응답 개체에 액세스할 수 있는 새 API NetworkAdInfo::getVastXml() 기능을 도입했습니다.

**버전 2.5.3**

Android™ TVSDK v2.5.3은 다음 업데이트 및 API 변경 사항을 제공합니다.

* CRS를 사용하는 모든 TVSDK 고객은 Android™에서 TVSDK 2.5.3.85 또는 최신 버전으로 앱을 업그레이드하는 것이 좋습니다. 기존 앱 구현의 드롭인 교체입니다. TVSDK 업그레이드 후 프록시 도구에서 CRS 크리에이티브 URL 요청을 확인합니다(예: Charles)를 사용하고 경로의 호스트 이름과 버전이 아래 샘플 URL 구조와 마찬가지로 반영되는지 확인합니다.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK의 사용자 에이전트 사용자 지정 가능: 사용자 에이전트를 사용자 지정하기 위해 새 API를 추가했습니다.

   * `setCustomUserAgent`(문자열 값)
   * `getCustomUserAgent`()

* Android™ Application과 TVSDK 간에 쿠키를 공유합니다. 이제 Android™ TVSDK는 Java™ 레이어(Android™ 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간 쿠키 액세스를 지원합니다. 이제 Java™ 쿠키 저장소에 노출되므로 네이티브 C++ 레이어에서 쿠키를 설정 및/또는 수정할 수 있습니다.
* API 변경 사항:

   * 새 이벤트 쿠키 UpdatedEvent가 추가됩니다. 쿠키가 업데이트되면 미디어 플레이어에서 발송됩니다.
   * 새 API가에 추가됩니다. `NetworkConfiguration::set/ getCustomUserAgent()` 사용자 지정 사용자 에이전트를 사용하려면
   * 새 API가에 추가됩니다. `NetworkConfiguration::set/ getEncodedUrlForTracking` 를 사용하여 안전하지 않은 문자를 강제로 인코딩합니다.
   * 새 API가에 추가됩니다. `NetworkConfiguration::getNetworkDownVerificationUrl()` 페일오버가 있는 경우 네트워크 확인 URL을 설정합니다.
   * 캡션을 표시하는 동안 공백을 영숫자로 처리할지 여부를 정의하는 TextFormat::treatSpaceAsAlphaNum에 새 속성이 추가됩니다.

* 의 변경 사항 `SizeAvailableEvent`: 이전에는 `SizeAvailableEvent` 미디어 형식에서 반환된 프레임 높이 및 프레임 너비를 반환하는 데 사용되는 2.5.2입니다. 이제 디코더에 의해 각각 반환된 출력 높이 및 출력 너비를 반환합니다.
* 버퍼링 동작의 변경 사항: 버퍼링 동작이 변경되었습니다. 버퍼가 비어 있는 경우 수행할 작업을 앱 개발자에게 남겨둡니다. 2.5.3은 버퍼 빈 상황에서 재생 버퍼 크기를 사용합니다.

**버전 2.5.2**

Android™ TVSDK v2.5.2는 중요한 버그 수정 및 몇 가지 API 변경 사항을 제공합니다.

**버전 2.5.1**

Android™ 2.5.1에서 릴리스된 중요한 새로운 기능입니다.

* **성능 개선**&#x200B;새로운 TVSDK 2.5.1 아키텍처는 몇 가지 성능 개선 사항을 제공합니다. 타사 벤치마킹 연구 결과를 기반으로 한 새로운 아키텍처는 업계 평균과 비교하여 시작 시간 5배 감소 및 3.8배 감소 프레임을 제공합니다.

   * **VOD 및 라이브 켜기 -** 인스턴트 온(instant on) 을 활성화하면 TVSDK가 미디어를 초기화하고 버퍼링한 후 재생이 시작됩니다. 백그라운드에서 여러 MediaPlayerItemLoader 인스턴스를 동시에 실행할 수 있으므로 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 재생이 즉시 시작됩니다. TVSDK 2.5.1은에 대한 Instant On도 지원합니다 **live** 스트림 도 참조하십시오. 라이브 창이 이동하면 라이브 스트림이 다시 작성됩니다.

      * **향상된 ABR 논리 -** 새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 속도 및 측정된 대역폭을 기반으로 합니다. 이렇게 하면 ABR에서 대역폭이 변경될 때 올바른 비트 전송률을 선택하고 버퍼 길이가 변경되는 속도를 모니터링하여 비트율 스위치가 실제로 발생하는 횟수를 최적화합니다.
      * **부분 세그먼트 다운로드 / 하위 세분화 -** TVSDK는 가능한 한 빨리 재생을 시작하기 위해 각 조각의 크기를 더 줄입니다. 해당 조각에는 2초마다 키 프레임이 있어야 합니다.
      * **레이지 광고 해상도 -** TVSDK는 재생을 시작하기 전에 프리롤 광고가 아닌 광고의 해상도를 기다리지 않으므로 시작 시간이 줄어듭니다. 모든 광고가 해결될 때까지 검색 및 트릭 플레이와 같은 API는 계속 허용되지 않습니다. 이는 CSAI와 함께 사용되는 VOD 스트림에 적용됩니다. 광고 해상도가 완료될 때까지 찾기 및 빠른 전방과 같은 작업이 허용되지 않습니다. 라이브 스트림의 경우 라이브 이벤트 동안 이 기능을 광고 해상도에 사용할 수 없습니다.
      * **영구 네트워크 연결 -** 이 기능을 사용하면 TVSDK에서 영구 네트워크 연결의 내부 목록을 만들고 저장할 수 있습니다. 이러한 연결은 각 네트워크 요청에 대해 새 연결을 열고 나중에 삭제하는 대신 여러 요청에 다시 사용됩니다. 따라서 네트워킹 코드의 효율성을 높이고 지연을 줄임으로써 재생 성능이 향상됩니다.
TVSDK가 연결을 열면 서버에 *생존* 연결. 일부 서버는 이 유형의 연결을 지원하지 않을 수 있습니다. 이 경우 TVSDK가 각 요청에 대해 다시 연결하는 데 실패합니다. 또한 영구 연결이 기본적으로 켜져 있지만 TVSDK에는 이제 앱이 원하는 경우 영구 연결을 끌 수 있는 구성 옵션이 있습니다.
      * **병렬 다운로드 -** 비디오 및 오디오를 직렬 대신 동시에 다운로드하면 시작 지연이 줄어듭니다. 이 기능을 사용하면 HLS Live 및 VOD 파일을 재생하고, 서버에서 사용 가능한 대역폭 사용을 최적화하고, 버퍼 언더런 상태로 전환될 가능성을 낮추며, 다운로드와 재생 사이의 지연을 최소화합니다.
      * **병렬 광고 다운로드 -** TVSDK는 광고 브레이크에 도달하기 전에 컨텐츠 재생과 동시에 광고를 미리 가져와서 광고 및 컨텐츠를 매끄럽게 재생합니다.

* **재생**

   * **MP4 컨텐츠 재생 -** TVSDK 내에서 재생하기 위해 MP4 짧은 클립을 다시 코딩할 필요가 없습니다.
참고: MP4 재생에는 ABR 스위칭, 트릭 재생, 광고 삽입, 지연 오디오 바인딩 및 하위 세그먼테이션이 지원되지 않습니다.
   * **응용 비트율(ABR)로 트릭 재생 -** 이 기능을 사용하면 TVSDK가 트릭 재생 모드에서 iFrame 스트림 간을 전환할 수 있습니다. iFrame이 아닌 프로필을 사용하여 빠른 속도로 트릭 재생을 수행할 수 있습니다.
   * **더욱 원활한 트릭 재생 -** 이러한 개선 사항은 사용자 경험을 향상시킵니다.

          * 대역폭 및 버퍼 프로필을 기반으로 트릭 재생 중 적응형 비트율 및 프레임 속도 선택
          * IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps의 빠른 재생.
      
* **컨텐츠 보호**

   * **해상도 기반 출력 보호 -** 이 기능은 재생 제한을 특정 해상도에 연결하여 보다 세밀하게 조정된 DRM 컨트롤을 제공합니다.

* **워크플로우 지원**

   * **직접 청구 통합 -** 이 작업은 고객이 사용하는 스트림에 대해 Adobe Primetime에서 인증한 Adobe Analytics 백엔드에 청구 지표를 전송합니다.
TVSDK는 고객 판매 계약을 준수하여 자동으로 지표를 수집하여 청구 용도로 필요한 주기적 사용량 보고서를 생성합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림 기간을 기반으로 컨텐츠 유형, 광고 삽입 활성화 플래그 및 drm 지원 플래그와 같은 청구 지표를 Adobe Analytics Primetime 소유 보고서 세트에 보냅니다. 이는 고객의 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하지 않거나 분석에 포함되지 않습니다. 요청 시 이 청구 사용량 보고서는 고객에게 정기적으로 전송됩니다. 사용 과금만 지원하는 청구 기능의 첫 번째 단계입니다. 설명서에 설명된 API를 사용하여 판매 계약에 따라 구성할 수 있습니다. 이 기능은 기본적으로 활성화되어 있습니다. 이 기능을 끄려면 참조 플레이어 샘플을 참조하십시오.
   * **향상된 페일오버 지원 -** 호스트 서버, 재생 목록 파일 및 세그먼트가 실패하더라도 중단되지 않고 계속 재생하도록 구현된 추가 전략입니다.

* **광고**

   * **해자 통합 -** 해자에서 광고 뷰가능 측정을 지원합니다.
   * **컴패니언 배너 -** 컴패니언 배너는 선형 광고와 함께 표시되며, 광고가 종료된 후에도 종종 보기에 계속 표시됩니다. 이러한 배너는 html(HTML 코드 조각) 유형이거나 iframe(iframe 페이지의 URL)일 수 있습니다.

* **Analytics**

   * **VHL 2.0 -** Adobe Analytics에 대한 사용 데이터의 자동 수집을 위해 최적화된 최신 비디오 하트비트 라이브러리(VHL) 통합입니다. API의 복잡성이 감소하여 구현을 쉽게 할 수 있습니다. VHL 라이브러리 다운로드 [Android™용 v2.0.0](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) 및 libs 폴더에서 JAR 파일을 추출합니다.

* **SizeAvailableEventListener**
   * 이제 SizeAvailableEvent의 getHeight() 및 getWidth() 메서드가 각각 높이 및 폭으로 출력을 반환합니다. 디스플레이 종횡비는 다음과 같이 계산할 수 있습니다.

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **쿠키**

   * 이제 Android™ TVSDK는 Android™ 애플리케이션의 CookieStore에 저장된 Java™ 쿠키에 대한 액세스를 지원합니다. 새 쿠키가 &quot;Set-Cookie&quot; 응답 헤더의 일부로 올 때마다 기록할 콜백 API(onCookiesUpdated)가 제공됩니다. 이러한 쿠키는 CookieStore를 사용하여 해당 특정 URI/도메인에 이러한 쿠키 값을 설정하여 다른 URI/도메인에 사용되는 HttpCookie 목록 으로 사용할 수 있습니다. 마찬가지로 TVSDK의 쿠키 값은 CookieStore 추가 API를 사용하여 업데이트됩니다.

## 기능 매트릭스 {#feature-matrix}

Android™용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

아래 기능 테이블에서 &#39;Y&#39;는 기능이 현재 릴리스에서 지원됨을 나타냅니다.

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생(재생, 일시 정지, 찾기) | VOD + Live | Y |
| FER - 일반 재생(재생, 일시 중지, 검색) | VOD 전송 | Y |
| 광고가 재생될 때 찾기 | VOD + Live | 지원되지 않음 |
| AC3 | VOD + Live | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | Y |
| 응용 비트율 전환 논리 | VOD + Live | Y |
| 오디오 전용 재생 | VOD + Live | Y |
| 다중 CDN 지원 | VOD + Live | 지원되지 않음 |
| 오디오 전용 미디어를 사용한 광고 재생 | VOD + Live | 지원되지 않음 |
| 닫힘 캡션 - 608/708 | VOD + Live | Y |
| 닫힘 캡션 - WebVTT | VOD + Live | Y |
| 매니페스트 장애 조치(Failover) | VOD + Live | Y |
| 고급 페일오버 | VOD + Live | Y |
| QoS 및 플레이어 알림 | VOD + Live | Y |
| 쿠키 헤더 지원 | VOD + Live | Y |
| 사용자 지정 HTTP 헤더 지원 | VOD + Live | Y(허용 목록 필수) |
| 버퍼 제어 매개 변수 설정 | VOD + Live | Y |
| 적응형 비트율 컨트롤 설정 | VOD + Live | Y |
| 사용자 지정 매니페스트 태그 | VOD + Live | Y |
| 늦게 오디오 바인딩 | VOD + Live | Y |
| 302 리디렉션 | VOD + Live | Y |
| 오프셋을 사용한 재생 | VOD + Live | Y |
| 오디오 전용 재생 | VOD + Live | Y |
| 트릭 플레이 | VOD + Live | Y |
| 트릭 플레이의 느린 동작 | VOD + Live | 지원되지 않음 |
| 부드러운 트릭 재생(ABR 사용) | VOD + Live | Y |
| ID3 구문 분석 | VOD + Live | Y |
| 광고 일시 중단 | VOD + Live | 지원되지 않음 |
| 즉시 켜기 | VOD + Live | 지원되지 않음 |
| 비연속성 마커 지원 | VOD + Live | Y |
| 302 리디렉션 고착성 | VOD + Live | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| 일반 재생, 광고 활성화 | VOD + Live | Y |
| 광고가 활성화된 FER 컨텐츠 | VOD | Y |
| 기본 광고 동작 | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4 광고 | VOD + Live | Y(CRS에서) |
| 광고가 활성화된 트릭 재생 | VOD + Live | Y |
| 광고 전용 | VOD | Y |
| 타깃팅 매개 변수 | VOD + Live | Y |
| 사용자 지정 매개 변수 | VOD + Live | Y |
| 사용자 지정 광고 동작 | VOD + Live | Y |
| 사용자 지정 광고 태그 | 라이브 | Y |
| 사용자 지정 광고 해상도 | VOD + Live | Y |
| Freewheel Custom Ad Resolver | VOD | Y |
| C3 | VOD + Live | 지원되지 않음 |
| 레이지 광고 해결 | VOD | Y |
| 불연속성 마커 지원 - SSSAI | VOD + Live | Y |
| 컴패니언 광고, 배너 광고 및 클릭 가능한 광고 | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y(JS) |
| 조기 광고 종료 | 라이브 | Y |
| 규칙 기반의 크리에이티브 우선 순위 지정 | VOD + Live | Y |
| CRS 규칙 | VOD + Live | Y |
| JSON Ad Resolver | VOD + Live | 지원되지 않음 |
| 해자 통합 | VOD + Live | Y |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| AES 암호화 | VOD + Live | Y |
| 샘플 AES 암호화 | VOD + Live | Y |
| 토큰화된 스트림 | VOD + Live | Y |
| DRM | VOD + Live | Primetime DRM만 해당(향후: Widevine) |
| 외부 재생(RBOP) | VOD + Live | Primetime DRM만 해당 |
| 라이선스 순환 | VOD + Live | Primetime DRM만 해당 |
| 키 회전 | VOD + Live | Primetime DRM만 해당 |

| 기능 | 컨텐츠 유형 | HLS |
|---|---|---|
| Adobe Analytics VHL 통합 | VOD + Live | Y |
| 과금 | VOD + Live | Y |

## 해결된 문제 {#resolved-issues}

해결 방법이 보고된 문제와 연결된 경우 Zendesk 참조가 표시됩니다(예: ZD#xxxxx).

**Android™ TVSDK 2.7**

이 섹션에서는 TVSDK 2.7 릴리스에서 해결된 문제에 대한 요약을 제공합니다.

* ZD#37166 - 광고가 잘 재생될 때에도 오류 추적 호출이 실행됩니다.
* ZD#37134 - VMAP 응답에 여러 광고가 있는 경우 래퍼(3P) 광고가 잘못된 광고 ID가 반환됩니다.

**Android™ TVSDK 2.5.6**

* ZD #34992 - 닫힌 캡션에서 언어가 비어 있습니다.
   * TVSDK가 캡션 추적 세부 정보를 가져오기 위해 기본 매니페스트에서 #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS를 구문 분석하지 않는 사례를 해결했습니다.
* ZD #35078 - Android P 유효성 검사.
   * TVSDK 2.5.6은 최신 Android™ P 베타 빌드로 확인되었습니다. 새 Android™ OS로 인해 문제가 없습니다.
* ZD #34149 - 오류가 발생하는 경우에도 플레이어가 매니페스트를 계속 요청합니다.
   * 모든 프로필이 다운되었을 때에도 TVSDK에서 반복 호출을 하는 문제가 수정되었습니다(404 오류).
* ZD #31533 - 앱을 백그라운드로 보낸 후 Android™에서 오디오를 재생합니다.
   * 추가됨 `enableAudioPlaybackInBackground` 앱이 백그라운드에 있을 때 오디오를 재생할 수 있도록 하기 위해 &#39;True&#39;를 인수로 사용하여 호출해야 하는 MediaPlayer의 API입니다(플레이어가 준비된 상태일 때).

**Android™ TVSDK 2.5.5**

* ZD #21647 - Android TVSDK는 실제 비디오 크기가 640x360이면 640x368에 알립니다.
   * 변수 m_nOutputHeight(AndroidMCVideoDecoder 내부)로 인해 실제 출력 높이 대신 프레임 높이로 업데이트됩니다. m_nOutputHeight를 올바르게 계산하기 위해 getVideoFrame 함수가 관련 변경 작업을 수행했습니다.
* ZD #26614 - Urgent — 타사 광고 서비스 / 프로그래밍 방식 — 노출 횟수 전달 실패
   * &quot;space&quot;가 &quot;equal&quot; 기호 앞에 있을 때 문제가 재현될 수 있는 XML 구문 분석에서 사례를 처리하여 이전 수정 사항을 개선했습니다. &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android: CRS 요청에 AdSystem 및 Creative ID를 추가합니다.
   * 이제 1401 및 1403 요청에 &#39;AdSystem&#39; 및 &#39;CreativeId&#39;를 새 매개 변수로 포함합니다.
* ZD #33062 - TVSDK는 CDATA 노드 아래에 있는 VAST 응답에서 파이프 문자 발생 시 충돌합니다
   * NetworkConfiguration 클래스의 API setEncodeUrlForTracking이 인코딩할 URL에 안전하지 않은 문자로 제거되었습니다.
* ZD #33063 - CRS 파일 선택 논리가 손상되었습니다. - TVSDK에서 웹 m 형식에 대한 CRS 요청을 보내지 않고 대신 3gpp 파일에 대해 CRS 요청을 전송했습니다.
   * 이제 논리를 수정했습니다. webm 및 3gpp 형식의 미디어 파일을 사용하는 경우 웹을 위해 CRS 요청을 전송합니다. 또한 3gpp 형식의 미디어 파일을 모두 사용하는 경우 가장 높은 비트율 3gpp 파일에 대해 CRS 요청을 전송합니다.
* ZD #33125 - Android 앱이 VMAP 내에서 특정 DoubleClick 태그와 충돌합니다.
   * 충돌을 방지하기 위해 시나리오를 수정했습니다.
* ZD #32256 - 라이센스 순환 및 키 순환 문제 - Adobe 액세스.
   * SampleAES 컨텐츠에 대한 DRM 메타데이터로 세그먼트 초기화를 수정했습니다. AES128 콘텐츠와 잘 작동합니다.
* ZD #33619 - 라이브 포인트와 가까운 버퍼링 상태에서 재생 목록 콘텐츠가 계속 성장하고 있습니다.
   * 트릭 재생 모드에서 라이브 포인트를 교차할 때 이 문제를 처리했습니다.
* ZD #34151 - TimedMetadata 개체 순서가 잘못되었습니다.
   * 타임라인에서 동일한 시간에 속했던 두 개의 TimedMetadata 이벤트가 임의로 표시됩니다. 그들의 원래 순서는 그대로 유지되었습니다.
* ZD #34189 - 광고 브레이크 시작을 시도할 때 문제가 발생합니다.
   * 불연속성을 사용하여 결합되는 SSSAI 광고에 문제가 있었습니다. 그리고 그 원인은 그러한 광고의 시작을 찾을 때, 키프레임을 검색하면 찾을 수 없는 동작이었습니다. 그 이유는 최소 비디오 타임스탬프보다 먼저 광고의 최소 오디오 타임스탬프가 존재하기 때문입니다. 따라서 잘못된 fragmentDump 데이터에서 키 프레임을 검색하게 됩니다. 지금 수정되었습니다.
* ZD #34528 - FireTV 3세대 동글의 640x360 이상으로 업그레이드하지 않는 비디오 해상도
   * 최신 펌웨어 업데이트를 포함하도록 수정 사항을 개선했습니다.
* ZD #34793 - TVSDK 2.5.x는 VideoEngine이 auditudeSettings를 사용할 수 있고 사용할 수 없다고 가정할 때 사용자 지정 컨텐츠 확인자와 충돌하는 데 사용되었습니다.
   * Null 공유 포인터(auditudeSettings)에 대한 함수 호출 때문에 충돌이 발생했습니다. VideoEngineTimeline::placeToSourceTimeline() 내에 해당 개체에 대해 모든 항목을 호출하기 전에 auditudeSettings를 사용할 수 있는지 확인하는 조건부 검사를 추가했습니다.
* ZD #32584 - &lt;extensions> VAST 응답의 노드.
   * XML 구문 분석과 관련된 문제가 해결되었으며 이제 NetworkAdInfo에서 &lt;extensions> 노드 아래에 있어야 합니다.
* ZD #35086 - 특정 VMAP 응답이 있는 경우 플레이어에서 전체 확장 데이터를 가져오지 않습니다.
   * 확장 xml에 특성 값 내에 큰 따옴표가 있는 경우 XML 구문 분석이 작동하지 않으므로 확장 xml에 문제가 있습니다. 문제가 해결되었습니다.

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 - Webview 원격 디버깅을 활성화하는 재생 세션.
   * WebViewDebuging은 기본적으로 False로 설정되어 있습니다. 디버깅을 사용하려면 setWebContentsDebuggingEnabled(true)를 사용하여 응용 프로그램을 통해 true로 설정합니다.
* ZenDesk#33011 - 실패한 CRS 요청이 있는 경우 광고 타임라인이 해결되지 않습니다.
   * 광고에 대한 CRS 요청이 실패하면 타임라인이 해결되고 나머지 광고가 재생됩니다.
* ZenDesk#34528 - 비디오 해상도는 FireTV 3세대 동글의 640x360을 넘지 않습니다.
   * 비디오 해상도는 비트율 스위치로 전환됩니다.
* ZenDesk#33192 - AudioUpdatedEventListener::onAudioUpdated를 통해 트랙을 검색할 때 AudioTrack의 이름이 null입니다.
   * FireTV Stick에 대한 몇 가지 시나리오에서 실제 오디오 업데이트가 없을 때 onAudioUpdate 이벤트가 실행되었습니다. 이제 수정되었습니다.

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata 사용자 지정 태그 구독이 작동하지 않습니다.
   * ID3 데이터를 바이트 배열(APIC 또는 일반 데이터 지원)으로 클라이언트에게 반환하고, 1.4 반환 문자열에서 바이트 배열은 null 종료 문자 자체를 처리하지 않으므로 클라이언트에 특수 문자를 표시했습니다. 이 문제가 해결되었습니다.
* Zendesk#32670 - 플레이어가 중복 재생 목록으로 페일오버되지 않음
   * 이 작업은 이제 제대로 작동하므로 setNetworkDownVerificationUrl이 예상대로 작동합니다.
* Zendesk#32369 - 닫힌 캡션은 다른 색상 가비지 또는 아티팩트를 표시합니다.
   * CC 결함 문제가 최신 빌드에서 수정되었습니다
* Zendesk#25590 - 개선 사항: TVSDK 쿠키 저장소(C++ to Java™)
   * 이제 Android™ TVSDK는 Java™ 레이어(Android™ 애플리케이션의 CookieStore에 저장됨)와 C++ TVSDK 레이어 간 쿠키 액세스를 지원합니다.
* Zendesk#32252 - TVSDK_Android_2.5.2.12가 PTPLAY-20269에 대한 수정 사항이 없는 것 같습니다. 이 문제가 해결되어 2.5.2 분기에 통합되었습니다.
* Zendesk#31806 - 응답 xml에 빈 태그가 있기 때문에 PREPARING Player의 Auditude 스틱이 준비 중 상태로 중단되었습니다. 이제 문제가 수정되었습니다.
* Zendesk#31727 - TVSDK 2.5 닫힌 캡션 문자가 삭제되거나 철자가 잘못되었습니다.
   * 문제가 해결되었으며 문자를 단락/잘못 삽입하지 않습니다.
* Zendesk#31485 - 2.5의 DrmManager
   * 새 DrmManager(컨텍스트 컨텍스트 컨텍스트)를 통해 DrmManager를 만드는 동안 문제가 발생했습니다. DRMManager를 제공하는 DRMService 클래스를 구현했습니다.
* Zendesk#32794- 1080P 해상도 스트림이 Android™에서 재생되지 않습니다.
   * SizeAvailableEvent를 변경했습니다. 이전에는 `getHeight()` 및 `getWidth()` 미디어 형식에서 반환된 프레임 높이 및 프레임 너비를 반환하는 데 사용되는 2.5의 SizeAvailableEvent 메서드입니다. 이제 디코더에 의해 각각 반환되는 출력 높이 및 출력 너비를 반환합니다.
* 세트 수준 매니페스트에서 #EXT-X-FAXS-CM 특성 위치로 인해 Zendesk #19359 Flash Player 충돌이 발생합니다.
   * #EXT-X-FAXS-CM 태그는 개별 비트율 또는 세그먼트가 재생 목록에 표시되기 전에 항상 맨 위 재생 목록에 나타나야 합니다.

**Android™ TVSDK 2.5.2**

* Zendesk#17305 불투명 배경의 닫힌 캡션의 아티팩트입니다.
TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* Zendesk#25097 CC 디스플레이에는 CC 설정이 있는 시각적 가공물이 있습니다.
TextFormat의 setTreatSpaceAsAlphaNum 속성이 노출됩니다. 기본적으로 속성은 False입니다. 어두운 공간 문제를 해결하려면 클라이언트에서 속성을 True로 설정합니다.

* Zendesk #31620 사용자 에이전트 문자열이 TVSDK 플레이어에서 나가는 것이 잘립니다.
사용자 에이전트 문자열은 128자 후에 더 이상 잘리지 않습니다.
Adobe Primetime 버전 문자열이 시스템 사용자 에이전트에 추가됩니다.

* Zendesk #30809 Missing SEEK_END 이벤트는 앱이 재생 상태로 전환되지 않도록 합니다.
* Zendesk #30415 Closed Caption의 &#39;Cyan&#39; 색상은 이전 Primetime TVSDK 릴리스와 비교하여 더 어두운 색의 파란색(터키색)입니다.

   색상이 DarkCyan에서 Cyan으로 변경되었습니다.

* Zendesk #30727 VOD 광고가 다운로드/해결되지 않습니다.

   VMAP XML에서 명시적 닫기 태그(&#39;)가 없는 빈 VAST 태그가 있는 경우&lt;/vast>&#39;) 및 줄바꿈 문자가 없는 경우 VMAP XML이 제대로 구문 분석되지 않고 광고가 재생되지 않을 수 있습니다.

**Android™ TVSDK 2.5.1**

* 장치별(삼성 갤럭시 탭 4) 충돌; Auditude를 사용하는 VOD DRM LBA를 클릭하고 광고를 클릭합니다.
* VHL - 오프셋에서 컨텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생되면 VHL 하트비트가 이벤트를 호출합니다:type:재생 광고가 누락되었습니다.
* 완료 상태로 전환되면 플레이어는 포스트롤 광고에 대해 SKIP adBreakPolicy를 사용하여 재생 상태로 돌아갑니다.
* 쿠키가 발신 광고 콜백에 첨부되지 않습니다.
* 광고 큐 포인트가 표시되지 않습니다.
* 별도의 EAC3 SAP 트랙이 있는 HLS가 로드되지 않습니다.
* Media Player가 복원된 후 TVSDK가 화면 켜짐 의도를 수신하면 플레이어가 충돌합니다.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7은 최대 5개의 광고 동시 해상도를 지원합니다.
* VMAP 응답의 경우, 단일 광고 브레이크에서 광고 호출이 동시에 수행되고 광고 브레이크가 순차적으로 해결됩니다.
* FER의 경우 각 기회의 광고 호출은 동시에 해결됩니다.

### 이전 릴리스의 알려진 문제 및 제한 사항{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* 여러 VMAP 광고 브레이크는 동시에 지원되지 않습니다.

**Android™ TVSDK 2.5.3**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에는 낮은 최종 장치에서 오디오-비디오 동기화 문제가 있거나 네트워크 상태가 좋지 않을 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER가 작동하지 않습니다.
* 지연 바인딩 오디오 컨텐츠를 찾을 때 재생이 중단될 수 있습니다.
* 간헐적으로 webVTT 캡션이 라이브 컨텐츠에 대해 동기화되지 않을 수 있습니다.
* 간헐적으로, 광고 브레이크에서 나온 후 몇 개의 프레임이 빠르게 재생될 수 있습니다.
* Ads가 재생되는 경우에도 Triple Wrapper Ad Break에 대해 303 오류가 발생하는 경우가 있습니다.

**Android™ TVSDK 2.5.2**

이 버전에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에는 저가 장치에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* VOD 미디어의 끝을 찾을 때 재생이 지연될 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER가 작동하지 않습니다.

**Android™ TVSDK 2.5.1**

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 라이브 비디오 재생에는 저가 장치에서 오디오-비디오 동기화 문제가 있을 수 있습니다.
* FER 스트림의 경우 virtualTime과 localTime이 다를 수 있습니다. 또한 오프셋이 있는 FER가 작동하지 않습니다.
* VMAP XML에서 명시적 닫기 태그(&lt;/vast>). 및 줄바꿈 없는 뒤에 VMAP XML이 제대로 구문 분석되지 않고 광고가 재생되지 않을 수 있습니다.
* VPAID 포스트롤은 지원되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* [시스템 요구 사항](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-requirements.html?lang=en)
* [Android™ Programmer&#39;s Guide용 TVSDK 2.7](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-overview-prod-audience-guide.html?lang=en)
* [TVSDK Android™ API용 Javadoc 참조](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android™ C++ API 문서](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - 각 Java™ 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 Java™ 문서보다 더 많은 설명서가 포함되어 있으므로 Java™ API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.
* [Android™(Java™) 마이그레이션 안내서용 TVSDK 1.4에서 2.5로](https://experienceleague.adobe.com/docs/primetime/migration/tvsdk-14-25-android.html?lang=en)
* 화면 켜짐/꺼짐 시나리오를 처리하려면 다음을 참조하십시오. `Application_Changes_for_Screen_On_Off.pdf` 빌드에 포함된 파일입니다.
* 에서 전체 도움말 설명서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지.
