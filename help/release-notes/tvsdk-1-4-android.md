---
title: Android용 TVSDK 1.4 릴리스 정보
seo-title: Android용 TVSDK 1.4 릴리스 정보
description: Android용 TVSDK 1.4 릴리스 정보에서는 TVSDK Android 1.4의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다.
seo-description: Android용 TVSDK 1.4 릴리스 정보에서는 TVSDK Android 1.4의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다.
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '7913'
ht-degree: 0%

---


# Android용 TVSDK 1.4 릴리스 정보 {#tvsdk-for-android-release-notes}

Android용 TVSDK 1.4 릴리스 정보에서는 TVSDK Android 1.4의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다.

## 새로운 기능 {#new-features}

**버전 1.4.43**

**HTTPS를 통한 안전한 광고 로딩**

Adobe Primetime은 HTTPS를 통해 Primetime 광고 서버 및 CRS에 대한 첫 번째 통화를 요청하는 옵션을 제공합니다.

**MediaPlayer 클래스의 alwaysUseAudioOutputLatency(boolean val)**

이 매개 변수가 설정되면 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용하십시오.

부울 매개 변수 값을 사용합니다. 이 값이 `True`이면 클라이언트는 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

**버전 1.4.42**

**부분 광고 중단 삽입:**
TV처럼 광고 중간에 끼어드는 경험을 어느 정도 시청한 광고에 대한 추적을 하지 않고 있는 것이다.
예: 사용자는 3개의 30초 광고로 구성된 90초 광고 중단의 중간(40초)에 참여합니다. 이것은 쉬는 동안 두 번째 광고에서 10초입니다.
* 나머지 기간(20초) 동안 두 번째 광고 다음에 세 번째 광고가 재생됩니다.
* 부분 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기가 실행됩니다.

**버전 1.4.41**

새로운 기능 없음

**버전 1.4.40**

새로운 기능 없음

>[!NOTE]
>
>1.4.39 이전 버전을 사용하는 경우 API 변경 사항이 필요하지 않습니다.

**버전 1.4.39**

* TVSDK는 VHL 2.0.1과 Nielsen과 함께 VHL 2.0.1을 인증하여 인증되었습니다.
* Android TVSDK가 새로운 Akamai 호스트에서 CRS 요청을 하도록 업데이트되었습니다 `primetime-a.akamaihd.net`.
* 새로운 호스트 이름 구성은 HTTP와 HTTPS(SSL)를 모두 통해 보다 큰 규모로 CRS 에셋 제공을 제공합니다.
* TVSDK는 Android Oreo 릴리스를 지원합니다.
* 여러 개의 기회 탐지기 등록을 지원하기 위해 새 함수가 `AdClientFactory` 클래스에 추가됩니다.

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   이 경우 PlacementOpportunityDetector 배열이 반환됩니다. 이제 여러 개의 기회 탐지기 등록을 할 수 있습니다. 예를 들어 초기 광고 종료 기능의 경우 광고 삽입에 대한 두 가지 기회 감지기(광고 조기 종료에 대한 한 가지)가 필요합니다. 이 새로운 기능은 DefaultAdvertisingFactory를 사용하지 않고 자신만의 AdvertisingFactory를 구현한 경우에만 구현되어야 합니다. 기존 비헤이비어를 얻으려면 createOpportunityDetector() 함수와 같이 단일 Opportunity Detector를 만들고 배열에 넣고 반환합니다.

   ```
   public class MyAdvertisingFactory extends AdvertisingFactory {  
   …  
   @Override  
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
   return opportunityDetectors;  
   } }
   ```

>[!NOTE]
>
>1.4.39 이전 버전을 사용하는 경우 API 변경 사항이 필요하지 않습니다.

**버전 1.4.36**

Android에서 내용 건너개에 대한 버그 수정.

**버전 1.4.35**

* **네트워크 광고 정보**

   이제 TVSDK API는 타사 VAST 응답에 대한 추가 정보를 제공합니다. 광고 ID, 광고 시스템 및 VAST 광고 확장 기능은 광고 자산의 networkAdInfo 속성을 통해 액세스할 수 있는 NetworkAdInfo 클래스에서 제공됩니다. 이 정보는 해자 Analytics과 같은 다른 광고 Analytics 플랫폼과 통합하는 데 사용할 **수 있습니다**.

**버전 1.4.31**

**CRS 광고에 대한 다중 CDN 지원**
* 기본적으로, 모든 코드 변환된 자산은 Akamai의 Adobe 소유 CDN에 호스팅됩니다. 최신 릴리스를 통해 Adobe CRS(Creative Repackaging Service)는 고객이 지정한 여러 CDN에 트랜스코딩 크리에이티브를 업로드할 수 있는 기능을 제공합니다.
* 기본 URL을 사용하지 않을 때 최종 CRS 크리에이티브 URL을 지정할 수 있도록 새 API가 TVSDK에 추가됩니다. 이러한 새로운 API를 사용하는 방법에 대해 알아보려면 설명서를 참조하십시오.

**버전 1.4.18** Primetime Android TVSDK는 이제 VPAID 2.0 Javascript 크리에이티브를 지원하므로 인터랙티브한 리치 인스트림 광고 경험을 제공할 수 있습니다. VPAID 2.0에 대한 자세한 내용은 VPAID [광고 지원을 참조하십시오](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**버전 1.4.17**

AC-3 5.1은 Amazon FireTV에서만 지원됩니다.

**버전 1.4.11**

* **광고 폴백, 광고 선택 로직 데이지 체인(Zendesk #3103** 폴백 규칙이 활성화된 VAST 광고(크리에이티브)의 경우, TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

자세한 내용은 VAST 및 [VMAP 광고에 대한 광고 폴백을 참조하십시오](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **비디오 하트비트 라이브러리(VHL)가 버전 1.5로 업데이트됨**
   * 비디오 시작 및/또는 비디오/광고/장 시작을 컨텍스트 데이터로 포함하는 메타데이터 전송
   * 네트워크 트래픽 감소 - 하트비트는 평균 감소 및 크기 감소

**버전 1.4.7**

* **온-프레미스 개인화**&#x200B;지원Adobe Personalization Server의 온-프레미스 설치를 지원하여 다른 종단점으로 가기 위해 고객의 개인화 요청을 사용자 지정합니다.

**버전 1.4.6**

* **샘플 AES 암호화(Flash Player 버전 17.0.0.134 필요)**샘플 기반 AES 암호화가 지원됩니다.

**버전 1.4.2**

* **VHL(비디오 하트비트 라이브러리)이 버전 1.4.0.1로 업데이트**

   * Adobe Analytics Video Essentials를 사용하여 다른 SDK 또는 플레이어에서 다양한 분석 사용 사례를 번들로 제공하는 기능을 추가했습니다.
   * trackAdBreakStart 및 trackAdBreakComplete 메서드를 제거하여 광고 추적을 최적화했습니다. trackAdStart 및 trackAdComplete 메서드 호출에서 광고 나누기가 유추됩니다.
   * 광고를 추적할 때 재생 헤드 속성이 더 이상 필요하지 않습니다.

* **Nielsen SDK**&#x200B;통합 이제 TVSDK는 사용자 정의 통합 없이 Nielsen SDK로 사용자 추적 정보 전송을 지원합니다.

**버전 1.4.0**

* **대체 컨텐츠 교체를** 통한 일시 중단 신호 1.4 TVSDK 업데이트의 일부로, TVSDK는 또한 선형 컨텐츠에 대한 지역 단전의 시작 및 재시작을 지원합니다. 이제 TVSDK에서 두 개의 매니페스트 파일을 병렬로, 주 및 대체 형식으로 처리할 수 있으므로, 원래 프로그래밍 대신 대체 프로그램이 보여지는 경우에도 정전 신호를 모니터링할 수 있습니다.

* **지금 C3 광고** 제거/바꾸기 C3 창에서 나오고 있는 VOD(Video-On-Demand) 자산에 새로운 광고를 동적으로 삽입하는 데 추가 준비 작업이 필요하지 않습니다. 이제 TVSDK에서 사용자 지정 컨텐츠 범위를 제거하고 새 광고를 동적으로 삽입하는 API를 제공합니다. 이 강력한 새로운 기능은 브로드캐스트 중에 라이브/선형 컨텐츠가 실행되고 에셋을 &quot;정리&quot;하는 데 적절한 시간 없이 on-demand 컨텐츠로 사용하기 위해 즉시 축소되는 경우에도 유용합니다.

* PlaybackEventListener 인터페이스에는 새 이벤트를 수신하기 위해 사용할 수 있는 onReplaceMediaPlayerItem이라는 새로운 메서드가 있습니다 `ITEM_REPLACED`. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스가 교체될 때마다 전달됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.
* AdClientFactory에는 여러 개의 기회 감지기에 등록하는 새 함수가 클래스에 추가되었습니다.

   public list&lt;PlacementOpportunityDetector> createOpportunityDetecers(MediaPlayerItem);

   예를 들어 초기 광고 종료 기능의 경우 광고 삽입에 대한 두 가지 기회 감지기, 일찍 종료하려면 각각 다른 감지기가 필요합니다 `ad`.

   이 새 함수를 재정의하려면 단일 Opportunity Detector를 만들고 배열에 넣고 반환합니다.

   @재정의

   public list&lt;PlacementOpportunityDetector> createOpportunityDetector(MediaPlayerItem mediaPlayerItem) {

   List&lt;PlacementOpportunityDetector> opportunityDetection = new ArrayList&lt;PlacementOpportunityDetector>();

   opportunityTendeers.add(createOpportunityDetector(mediaPlayerItem));

   return opportunityDetector;
}

   }

## 1.4에 대한 TVSDK 변경 사항 {#tvsdk-changes}

* PlaybackEventListener 인터페이스에는 새 이벤트인 ITEM_REPLACED를 수신하는 데 사용할 수 있는 onReplaceMediaPlayerItem이라는 새로운 메서드가 있습니다. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스가 교체될 때마다 전달됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.

* AdClientFactory에는 여러 개의 기회 감지기에 등록하는 새 함수가 클래스에 추가되었습니다.

public list createOpportunityDetecers`<PlacementOpportunityDetector>` (MediaPlayerItem);

예를 들어 초기 광고 종료 기능의 경우 광고 삽입에 대한 두 가지 기회 감지기(광고 조기 종료에 대한 측정기 하나)가 필요합니다.

이 새 함수를 재정의하려면 단일 Opportunity Detector를 만들고 배열에 넣고 반환합니다.

@재정의

공개 목록`<PlacementOpportunityDetector>` createOpportunityDetecers(MediaPlayerItem) {

목록`<PlacementOpportunityDetector>` 기회 감지기 = 새로운 ArrayList`<PlacementOpportunityDetector>`();

opportunityTendeers.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetector;

}

}

## 1.4의 장치 인증 및 지원 {#device-certification-and-support-in}

>[!NOTE]
>
>다음 기능은 TVSDK에서 지원되지 **않습니다** .
>
>* 모든 플랫폼 또는 버전에서 슬로우 모션 제작
>* 라이브 트릭 플레이


**버전 1.4.43**

TVSDK 1.4.43은 Android 6.0.1/7.0 및 8.1(Oreo)을 사용하는 Android 디바이스에서 인증되었습니다.

* **버전 1.4.23:**

   * TVSDK 1.4.23은 Android N 기반의 Android 디바이스에서 인증되었습니다.

* **버전 1.4.18:**

   * Primetime은 Amazon Fire TV에서 인증되었습니다.
   * VPAID 2.0은 Android 4.0 이상의 디바이스에서만 지원됩니다.

## 1.4에서 해결된 문제 {#resolved-issues-in}

>[!NOTE]
>
>CRS를 사용하는 모든 TVSDK 고객은 iOS 및 Android 기반의 TVSDK 1.4.39 또는 최신 버전으로 업그레이드할 것을 적극 권장합니다. 이 업그레이드는 기존 앱 구현에 대한 드롭인 대체입니다. 업그레이드 후 프록시 도구(예: Charles)에서 CRS 크리에이티브 URL 요청을 확인하여 경로의 버전이 버전 3.1을 반영하는지 확인합니다. 예:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**버전 1.4.43**

* 티켓 번호 27143 - FireTV 장치에서 5.1 오디오 트랙을 재생할 수 없음

   * 이제 TVSDK에서 FireTV 장치에서 AC3 오디오를 재생할 수 있습니다. 재생은 항상 스테레오로 이루어집니다.

* 티켓 번호 33902 - HTTPS를 통한 안전한 광고 전달

   * Adobe Primetime은 https를 통해 Primetime 광고 서버 및 CRS에 대한 첫 번째 통화를 요청하는 옵션을 제공합니다.

* 티켓 번호 34493 - Bluetooth 오디오 지연

   * 설정할 때 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용하게 되는 MediaPlayer 클래스에 추가되었습니다. `alwaysUseAudioOutputLatency`

* 티켓 번호 34949 - 새로운 버전의 VHL(비디오 하트비트 라이브러리)이 통합되었습니다.

**버전 1.4.42(1791)**

* Zendesk #33719: FireTV 4k 적응형 비트 전송률은 느리게 조정됩니다. FireTV 4K 장치용 ABR에 대한 지원을 추가했습니다.
* Zendesk #3338:  resetDRM은 응용 프로그램의 모든 데이터를 지웁니다.  비-TVSDK 스레드의 예외로 인해 TVSDK 작업 큐가 채워지는 경우를 추가로 처리했습니다.

**버전 1.4.41(1776)**

* Zendesk #33002 - Fire TV에서 TVSDK와 함께 사용 가능한 에셋 데이터 Companion 데이터를 List &lt;AdBannerAsset> 및 AdAsset::id로 반환하는 새 클래스 AdBannerAsset이 구현되었습니다.
* Zendesk #32821 - Android Primetime 플레이어는 WWE용 PTS(프레젠테이션 타임스탬프)가 나타나면 멈춥니다. 이 문제는 이번 릴리스에서 해결되었습니다.
* Zendesk #33572 - VideoAnalyticsProvider 광고 시작 충돌. VideoHeartbeat.jar의 VHL+Nielsen 공동 SDK 버전의 올바른 조합을 사용하여 이 문제를 수정했습니다.
* Zendesk #33355 - Fire TV: 15초 발행물 스크러빙 TVSDK 측에서 수정할 사항이 없으며 고객은 최종 사용자 및 타사 웹 사이트에서 이 문제를 확인하고 있습니다.

**버전 1.4.40(1764)**

* Zendesk #33068 - 새 장치의 Amazon 립싱크 문제 이 릴리스에서는 립싱크 문제가 해결되었습니다.
* Zendesk #32215 - Android TVSDK 1.4.38 보안 문제 `[Hotlist]`. 최신 OpenSSL-1.1.0 및 curl-7.55.1로 업데이트되었습니다.
* Zendesk #32920 - 광고 중단 내에 빈 화면이 있고 광고 중단 이수 없습니다. VPAID 컨테이너가 중단 상태로 전환되고 Facebook VPAID 광고가 단일 \&amp;lt;AdParameters\&amp;gt; VAST 노드.

**버전 1.4.39(1744)**

* Zendesk #28976 - 라이선스 요청을 완료하는 데 1초 이상이 소요됩니다. POST를 사용하는 DRM 라이센스 요청 호출이 실행 중일 때 Curl은 &quot;예상: 100-continue&quot; 헤더. TVSDK에서 &quot;예상:&quot; 헤더가 제거되었습니다.
* Zendesk #27707 - CSAI 환경에서 일찍 돌아오거나 컨텐츠로 돌아가기 위해 CUE IN 마커를 사용하지 않습니다. 여러 기회 생성기에 대한 지원을 제공했습니다.

**버전 1.4.38(1722)**

* Zendesk #21590 - 최신 원본 빌드의 비디오 성능 및 추적

TVSDK에서 VHL 2.0을 통합 및 인증하여 API의 복잡성을 줄임으로써 VideoHeartbeatsLibrary 구현의 장벽을 줄일 수 있습니다.

* Zendesk #29688 - Android O 베타 고객 지원

새로운 Android 베타 릴리스에 대한 TVSDK 지원

**버전 1.4.36(1713)**

* Zendesk #27392 - Android에서 컨텐츠 건너뛰기

암호 해독을 위해 Android TVSDK가 비프레임 컨텐츠의 바이트 범위를 16바이트로 잘못 확장했습니다. 확장 기능은 Iframe 스트림에 필요하지만 비프레임 스트림에는 필요하지 않습니다.

**버전 1.4.34(1702)**

* Zendesk #27638 - cURL INet 개체 누수

cURL 연결에 사용한 공유 관리자와 DNS 캐시를 유지하는 동안 Posix cURL INet 개체가 새어 나갔습니다.

이 문제는 INet 해체기에서 Posix cURL INet 개체를 삭제하여 해결되었습니다.

**버전 1.4.33(1694)**

* **OpenSSL 라이브러리**

OpenSSL 라이브러리가 OpenSSL 버전 1.0.2j로 업데이트되었습니다.

* Zendesk #21701 - 정규화된 URL 대신 1401 CRS 요청에 대한 원본 크리에이티브 URL을 전송합니다.
이 문제는 원래 크리에이티브 URL을 전송하여 해결됩니다.

* Zendesk #25023 - 비디오 재생 시간: 비디오 고정, 화면 flickr이 문제는 CenturyLink 셋톱 박스 장치의 최대 비디오 형식 크기를 설정하여 해결되었습니다.

* Zendesk #27460 - 새 Akamai 계정이 POST CDN 요청을 처리할 수 없습니다.
광고 요청이 POST 대신 GET이 되도록 `cdn.auditude.com` 코드가 업데이트되었습니다.

* Zendesk #28245 - 앱이 백그라운드에서 전면으로 전환될 때 재생 상태에 제대로 알림이 되지 않습니다. 응용 프로그램이 전면으로 돌아갈 때 재생 또는 일시 정지하도록 재생 상태를 올바르게 복원하여 이 문제가 해결되었습니다.

**버전 1.4.32(1682)**

* Zendesk #25779 - WebView에서 JavaScript를 사용하는 경우 TVSDKAndroid 4.2 이하에서 발견된 보안 취약성이 보안 취약성을 갖습니다. OS 4.2 이하를 실행 중인 장치에 대해 TVSDK별 WebView 사용을 비활성화했습니다. 이렇게 하면 이러한 장치의 TVSDK에서 VPAID 광고 사용이 비활성화됩니다.

* Zendesk #26890 - Ref 처리 화면 상태(설정/해제) 문제 플레이어Adobe 비디오 엔진(AVE)이 일시 중단 상태에서 다시 시작되면 DefaultMediaPlayer가 해당 상태를 업데이트하지 않습니다. 따라서 AVE가 재생 중인 상태임에도 불구하고 DefaultMediaPlayer는 일시 중단 상태로 유지됩니다. AVE로부터 재생 상태를 받을 때 DefaultMediaPlayer 상태를 PLAYING으로 설정하여 DefaultMediaPlayer의 현재 상태가 SUSPENDED인 경우에도 이 문제가 해결되었습니다.

**버전 1.4.31(1675)**

* Zendesk #21974 - null 개체 때문에 예외가 발생했습니다.
   * AdIndex는 null일 때 증가되는 경우가 거의 없습니다. 이는 프리롤 adBreak에 대해 수신된 잘못된 API 호출 때문일 수 있습니다. 이러한 예외를 피하도록 데이터 유형을 수정했습니다.

* Zendesk #24714 - 외부 로깅 해제
   * 외부 로깅(logging)을 끄도록 TVSDK를 업데이트했습니다.

* Zendesk #24488 - Fire TV의 AV 동기화 문제
   * AV 디코더 스레드 처리를 개선하여 수정했습니다. 특히 입력 또는 출력 프레임 큐가 수정될 때마다 프레임의 컨텐츠 유형에 맞는 디코더 스레드가 실행됩니다.

* Zendesk #26551 - CRS 오류 수정
   * 요청이 HEAD(http head)이면 비어 있으므로 해당 콘텐츠를 읽을 필요가 없습니다. 읽어도 괜찮지만 read()를 호출하면 이전 Android(4.0.x)가 정지되고, 읽기()를 호출하면 최신 Android 반환 올바른 값(-1)이 반환됩니다. 이에 따라 코드가 &quot;head&quot;에 대한 컨텐츠를 읽지 않도록 변경되었습니다.

* Zendesk #26696 TrickPlayManager 액세스 시 Null 포인터 예외
   * TrickPlayManager 개체를 사용하기 전에 null이 아닌지 확인하여 수정했습니다.

**버전 1.4.30(1659)**

* Zendesk #22675 자산 지속 시간이 라이브/선형 스트림에 대해 업데이트되지 않습니다. 이 문제는 라이브 및 선형 스트림의 자산 지속 시간을 제공하는 PTVideoAnalyticsTrackingMetadata에 새 API, assetDuration을 제공하여 해결되었습니다.

* 채널 전환 시 Zendesk #25853 TVSDK의 메모리 누수MediaPlayer가 재설정되거나 파일 다운로드 중 해제되는 경우 파일 읽기 버퍼 누수가 발생하는 문제가 해결되었습니다.

**버전 1.4.29(1653)**

* Zendesk #21200 - 앱이 백그라운드에 있을 때 플레이어가 일시 중단 상태로 복구되지 않습니다. 스트림 전환이 신호를 받은 후 플레이어가 일시 중단되었을 때 해상도는 플레이어가 이전 위치로 복원하는 대신 일시 중단 상태에서 플레이어를 복원할 때 스트림 스위치를 수행할 수 있도록 합니다.

* Zendesk #23412 - 광고 중단 기간의 마지막 3초 내에 모든 광고를 클릭하는 경우 플레이어에 검정색 박스가 붙어 있습니다. 이 문제는 Zendesk #21200과 동일한 문제입니다.

* Zendesk #23616 - 생략된 광고 나누기가 너무 먼 미래를 찾습니다광고 삽입 유형(삽입/바꾸기)에 따라 TVSDK는 광고 지속 시간을 계산에 사용하여 광고 중단 끝점을 결정하는지 여부를 결정합니다.

* Android TV STBT의 TVSDK DRM 메모리 누수DRM 어댑터 개체의 메모리 누수가 위치 및 수정되었습니다.

* Zendesk #25067 - VideoEngineTimeline개체가 올바르게 정리되지 않고 개체가 제거된 후에 이벤트가 호출되었기 때문에 충돌이 발생합니다. null 예외를 방지하기 위해 검사를 추가하여 문제가 해결되었습니다.

* Zendesk #25352 - 사용자 지정 HTTP 헤더 설정이 문제는 TVSDK의 허용 목록에 새 사용자 지정 헤더를 추가하여 해결되었습니다.

* Zendesk #25617 - 플레이어 중단 및 메모리 충돌을 일으키는 라이브 스트림 PTS 롤오버 이 세그먼트 중간에서 롤오버가 발생할 때 PijandedHTTPStreamer에 PTS 롤오버 처리를 추가하여 이 문제를 해결했습니다.

**버전 1.4.28(1637)**

* 광고 정책 상담 전에 광고 중단 이벤트 발생 adCompletion으로 인해 광고를 건너뛸 때 AD_BREAK_START 및 AD_START 이벤트를 시작하지 않아 이 문제가 해결되었습니다. AD_BREAK_BRADDED 이벤트가 대신 전송됩니다.

**버전 1.4.27(1631)**

* Zendesk #23174 - 비디오 크기 조정 시 성능 문제 이 문제는 TVSDK가 MediaPlayerView에서 SurfaceHolder.setFixedSize()에 액세스할 수 있는 새 API인 MediaPlayerView.setFixedSize()를 입증하여 해결되었습니다.

* Zendesk #24450 - TVSDK에서 중복 광고 요청을 처리함 이 문제는 경과된 시간이 2배가 아니라 길이로 변환되어 이 문제가 해결되었습니다.

**버전 1.4.26(1627)**

* Zendesk #21436 - OpenSSL 라이브러리 업데이트 버전 1.0.2h OpenSSL 라이브러리를 OpenSSL 버전 1.0.2h로 업데이트했습니다.
* Zendesk #23825 - Android 쿠키에 대한 지원을 제공함으로써 쿠키가 콜백에 포함되지 않습니다.

**버전 1.4.25(1620)**

* Zendesk #22900 - 라이브 Adobe Primetime DRM 스트림이 Android 참조 플레이어에서 재생되지 않고 있습니다. 메모리 할당 문제가 해결되었습니다.
* Zendesk #23176 - VPAID 광고를 재생하려고 할 때 애플리케이션이 충돌합니다. 애플리케이션이 사용자 지정 광고 보기를 만들지 않아 VPAID 광고를 렌더링하지 못했습니다. 이 문제는 사용자 지정 광고 보기가 없을 때 광고 서버 응답의 VPAID 광고를 무시함으로써 해결되었습니다.

* Zendesk #23153 - SampleAES DRM Stream - TVSDK Reference Player에서 재생 지연이 문제인 Zendesk #22900과 동일합니다.

**버전 1.4.24(1612)**

* Zendesk #20784 - Analytics: 라이브 비디오 전환을 위한 콘텐츠 트리거 완료이 문제는 라이브/선형 비디오 추적 세션 중에 컨텐츠의 완료를 수동으로 트리거하도록 API(trackVideoComplete)를 추가하여 해결되었습니다.

* Zendesk #21977 VideoEngineTimeline Crash during placeAdBreak/acceptAd 작업
   * 이 문제에서는 다음 라이브러리가 업데이트되었습니다.
      * AdobeMobile 라이브러리를 버전 4.10.0으로 변환
      * VHL 라이브러리를 버전 1.5.6으로 변환
      * VHL-Nielsen 라이브러리를 버전 1.6.7로 변환

이 문제는 승인된 광고 목록에 광고를 추가하기 전에 null 검사를 추가하여 해결되었습니다.

* Zendesk #22313 Amilogic 칩셋이 설치된 STB의 비트 전송률은 1.2MT미디어 코덱을 미리 로드하고 Amilogic 칩셋 디바이스에 대한 매끄러운 스위치를 비활성화하여 문제를 해결했습니다.

* TVSDK 플레이어에서 재생되지 않는 샘플 AES HLS 에셋이 #19520 샘플 AES 암호화된 HLS 스트림에 대해 여러 PMT 설명자를 처리하여 이 문제가 해결되었습니다.

**버전 1.4.23(1602)**

* Zendesk #18852 - CRS 규칙에 따라 크리에이티브 선택 논리 업데이트이 문제는 JSON 구성 파일을 추가하여 크리에이티브 선택 우선 순위를 지정하여 해결되었습니다.

* Zendesk #20861 - Android NT이 릴리스는 Android N에서 실행되는 응용 프로그램에서 더 이상 액세스할 수 없는 Android 플랫폼 기본 라이브러리를 직접 사용하는 기능을 제거하여 Android N을 지원합니다.

* Zendesk #21018 - Android N 충돌 ZD# 20861과 동일한 해상도

* Zendesk #21266 - VideoEngineAdapter 충돌 Invalid_Key 오류Invalid_Key 오류는 AVE의 설명을 포함하지 않으므로 텍스트를 구문 분석하여 NPE로 연결되었습니다. 설명을 구문 분석하기 전에 onError 중에 설명에 대해 null 검사를 추가하여 문제를 해결했습니다.

* Zendesk #22286 - 기본 라이브러리가 메모리 읽기 키/조각 작업을 할당하는 중 충돌을 발생시킵니다. 여러 키를 동시에 사용하여 매니페스트를 로드하려고 할 때 Android에서 발생한 이 충돌이 해결되었습니다.

**버전 1.4.22(1581)**

* Zendesk #17236 - DRMT가 있는 HLS 비디오에 대한 안정적인 재생 헤드 타임 오디오 세그먼트 시작 시간이 비디오 세그먼트 시작 시간과 일치하지 않는 LBA 스트림으로 시간 이동 문제가 수정되었습니다.

* Zendesk #17680 - Video playback is freezing on the Selection Andredo box이 장치의 비디오 디코더는 때때로 출력 버퍼에서 비디오 프레임을 대기할 때 상당한 출력 시간 이동을 반환하고 이 출력 타임스탬프는 높은 값으로 유지됩니다. 이 문제는 플레이어가 동일한 프로필을 다시 시도하거나 다른 프로필을 선택하도록 강제하지 않는 *비디오 프로필을 지원하지* 않는 오류를 반환하여 해결되었습니다.

* Zendesk #19074 - FWD 및 REW 트릭 재생 중 비디오 멈춤 이 문제는 새로운 경고 TRICKPLAY_ENDED_DUE_TO_ERROR를 추가하여 응용 프로그램에 트릭플레이가 종료되었으며 복구할 수 없는 오류로 인해 비디오가 일시 중지되었음을 알려 줍니다.

* Zendesk #19574 - TVSDK가 DRM 또는 비 DRM 컨텐츠에 대한 M3U8 응답 데이터를 반환하지 않습니다. 이 문제는 다음과 같은 방법으로 해결되었습니다.

* Zendesk #19986 - Android TV와 같은 특정 장치에 대한 OP 동작 깨짐
* 조건에 FILE_NOT_FOUND 오류를 추가하는 중입니다.
* 찾을 수 없는 *파일* 오류로 인해 오류가 발생하면 URL과 응답을 사용할 수 있는 경우 오류 설명에서 구분합니다.
NVidia shield OP 지원에 의해 도입된 논리 오류가 수정되었습니다. NVidia가 아닌 장치에서 표시 유형을 알 수 없는 경우에도 표시 보안 플래그를 신뢰합니다.

* Zendesk #20549 - 오래된 재생 목록 처리 이전 가져오기에 새 세그먼트가 수신되지 않을 경우 라이브 매니페스트 업데이트 사이의 간격을 예상 세그먼트 기간의 반으로 줄여 이 문제가 해결되었습니다.

* Zendesk #20742 - FireTV에서 라이브 컨텐츠를 재생할 때 메모리 사용이 계속 증가하고 있는 것으로 나타납니다.충돌을 일으키는 JNI 객체 참조 테이블이 제한에 도달했기 때문입니다. 디코더 다시 시작 중에 생성된 MediaFormat 개체에 대한 참조를 삭제하여 이 문제가 해결되었습니다.

* Zendesk #21125 - CSAI(라이브/선형 광고 중단)에서 일찍 돌아오십시오. 플레이어에서 기회 탐지기 기능을 사용하여 광고 큐에 스플릿을 등록하는 경우 광고 중단 동안 플레이어가 주 컨텐츠로 돌아갈 수 있도록 하는 기능을 추가했습니다.

* Zendesk #21334 - TVSDK 및 타사 광고 요청에 대한 요청 시간 초과 값. 광고 호출에 대한 전역 시간 초과를 활성화하는 adRequestTimeout 설정이 AdvertisingMetadata에 추가되었습니다.

**버전 1.4.21(1566)**

* Zendesk #17781 - ADB 화면 캡처가 더 이상 작동하지 않습니다. 이 문제는 화면 캡처를 허용하는 DefaultMediaPlayer.create(Context, boolean secureSurface) API를 추가하여 해결되었습니다.
화면 캡처를 허용하려면 secureSurface에 대해 false를 전달합니다.
중요: 프로덕션 설정에서 이 화면 캡처 기능을 활성화하지 않는 것이 좋습니다.

* Zendesk #19074 - FWD 및 REW 트릭 재생 중 비디오 동결재생

* Zendesk #19532 - 닫기 캡션이 잘못 표시되었습니다.
   * FHS가 조금씩 움직이기 시작하지만 첫 번째 iframe 세그먼트에 프레임이 없었습니다.
   * iframe 세그먼트를 다운로드하는 동안 FHS에서 오류 조건이 발생하면 trickplay에서 종료되고 재생을 일시 정지합니다.
   * Android MediaCodec 구현은 모든 입력/출력 버퍼를 플러시하라는 요청을 받는 동안 입력 큐 가용성을 항상 기다립니다.
이 문제는 겹치는 여러 큐가 &quot;위로 스크롤&quot;하는 것처럼 표시되도록 WebVTT 큐의 순서를 반전하여 해결되었습니다.

* Zendesk #19574 - TVSDK가 DRM 또는 비-DRM 컨텐츠에 대한 M3U8 응답 데이터를 반환하지 않습니다.PTMediaPlayerItem.prepareToPlay의 매니페스트 파일의 초기 로드에서 로딩에 실패할 경우 TVSDK가 애플리케이션에 대한 실패 응답 본문을 보고하지 않습니다.
이 문제는 TV SDK가 오류 응답을 응용 프로그램에 보고하도록 허용하여 해결되었습니다.

* Zendesk #19701 - SAP/Discontinuity오디오 및 비디오가 중단 시 정렬되지 않은 경우 재생이 멈춥니다.

* 버그 #PTPLAY-11162 - 버전 1.0.2f에 대한 OpenSSL 라이브러리 업데이트가 해결되었습니다.

**버전 1.4.20(1546)**

* Zendesk #17384 - 기능 요청: AAC 미디어의 ID3 태그에 대한 ID3 메타데이터 지원이 버전 1.4.20부터 Android용 TVSDK에서 제공됩니다.

* Zendesk #18358 - 플레이어가 동기화되지 않은 동기화 불연속성의 비트 전송률 스위치에서 멈춥니다. 이 문제는 ABR 연결 에지 사례를 적절하게 처리하여 해결되었습니다.

* Zendesk #19232 - 이전 Amazon OS 버전 4에서는 TVSDK 1.4.18을 사용하는 앱이 이상하게 작동합니다. 이 문제는 Android Webview를 지원하지 않는 장치와의 충돌을 방지하기 위해 TVSDK 플레이어 초기화 프로세스에서 숨겨진 웹 보기 만들기를 제거하여 해결되었습니다.

* 적응형 비트 전송률 전환이 발생할 때 Zendesk #19585 - 슬로우 모션 재생
ABR 스위치 중 새 프로파일의 오디오 샘플 속도가 현재 프로파일과 다른 경우 재생이 빨라지거나 속도가 느려집니다. 오디오 형식이 변경되었다는 알림을 비디오 발표자에게 보내지 않기 때문입니다.
이 문제는 알림 플래그가 올바른 위치에 설정되어 있는지 확인하여 해결되었습니다.

* Zendesk #19683 - SAP DAI 재생 - 몇 초 동안 오디오가 없습니다.
TVSDK 로직에서의 여러 경우 두 변환 세그먼트의 타임스탬프를 비교할 때 타임스탬프가 항상 0ms 차이와 일치할 수 없기 때문에 RENDITION_TIMEOUT_THRESHOLD가 허용되는 값 범위로 사용되었습니다. 간격이 RENDITION_TIMEOUT_THRESHOLD 범위 내에 있는 경우 일치하는 것으로 가정합니다.

RENDITION_TIMEOUT_THRESHOLD가 100ms로 설정되었지만 특정 스트림에 부족한 것으로 발견되었습니다. 이 문제는 RENDITION_TIMEOUT_THRESHOLD를 200ms로 늘려 해결되었습니다.

* Zendesk #19699 - TVSDK가 VTT 자막 트랙 간을 전환할 수 없습니다. 이 문제는 트랙 변경 시 플레이어 덤프를 만들고 매니페스트를 다시 로드하여 해결되었습니다. 이 문제는 2바이트 WebVTT 자막 트랙 이름에 영향을 준 UTF8 문자열 변환 문제를 수정함으로써 해결되었습니다.

* Zendesk #19717 - CC 옵션 표시 문제유니코드 문자열을 올바르게 처리하여 이 문제를 해결했습니다.

* Zendesk #19910 - TIT2 ID3 태그가 없습니다. 이 문제는 ID3 v2.4 문자열 인코딩에 대한 완벽한 지원과 ID3 v2.3을 지원하여 해결되었습니다.

* Zendesk #20135 - TVSDK가 VOD 컨텐츠에 대해 다중 onComplete를 트리거하고 있습니다.
이 문제는 상태 변경 이벤트의 전체 사례 대신 적절한 위치에 post_roll_complete 이벤트 리스너를 추가하여 해결되었습니다.

**버전 1.4.19(1521)**

* Zendesk #4180 - TVSDK가 HDCP를 시행하지 않습니다.
   * 이 티켓에 대한 부분 수정이며 NVidia 실드 장치의 문제만 해결합니다.
HDCP 상태를 동적으로 추적하려면 Nvidia Shield에서 올바르게 구현된 HDCP 감지 API를 사용해야 합니다.

* Zendesk #18358 - TVSDK가 동기화 불연속성이 없는 비트 전송률 스위치에서 고정됩니다.
   * 이 문제는 PTS 불연속성을 탐지하기 위한 새로운 경고를 추가하고 PTS 검사를 강제로 수행하여 모든 ABR 스위치에 대해 올바른 세그먼트 검색을 다시 실행함으로써 해결되었습니다.
고정 문제를 해결하려면 mediaPlayer.setCustomConfiguration 메서드에 대한 호출에는 forcePTSCheckForABR을 인수로 포함해야 합니다.

* Zendesk #19038 - Asus Zenpad 10에는 라이브 스트림이 없습니다.

   이 문제는 런타임에 함수를 쿼리하지 않도록 미디어 코덱을 미리 로드하여 해결되었습니다.

* 다음 문제는 Zendesk #19038과 동일합니다.
   * Zendesk #19483 - TVSDK가 인텔 플랫폼에서 충돌하고 있습니다.
   * Zendesk #19171 - Android 5.0이 있는 Asus Memo Pad 7에서 충돌이 발생했습니다.

**버전 1.4.18(1503)**

* Zendesk #3324 - Primetime 광고 보고는 VMAP에 광고 미디어가 없을 때 광고 중단을 추적하지 않습니다.
광고 브레이크가 비어 있으면 광고 중단 시작 및 전체 추적 이벤트가 핑되지 않았습니다. 이 문제는 유효한 AdSource 쌍으로 VMAP AdBreak와 같은 빈 광고 중단에서 광고 중단 시작 페이지를 전송하여 해결되었습니다.

* Zendesk #18229 - SetCCVisability(VISIBLE)는 MediaPlayer.reset() 호출 후에 무시됩니다. 이 문제는 setCCVisability(Visible.INVISIBLE)를 추가하여 해결되었습니다. 를 MediaPlayer 클래스에 있는 reset() 함수에 넣습니다.

* Zendesk #18328 - 60FPST가 있는 컨텐츠에 대한 Amazon Fire TV 2세대 장치의 프레임 문제가 해결되었습니다. 이 문제는 절전 시간 결정 시 FPS를 적용하여 보다 향상된 인코딩 FPS 예측 논리를 적용함으로써 해결되었습니다.

**버전 1.4.17(1472)**

* Zendesk #2231 - MediaPlayerNotification에서 사용할 수 없는 매니페스트를 가져올 때 반환된 오류 구문 분석 오류가 있을 때 매니페스트의 응답 본문을 포함하여 이 문제가 해결되었습니다.

* Zendesk #17703 - VideoEngineView는 비디오 재생 중에 스크린샷을 방지할 수 없습니다. setSecure 메서드는 API 17부터 사용할 수 있지만 API 17은 4.2, 4.2.1 및 4.2.2를 적용하므로 예외를 throw할 사람이나 장치별 여부를 알 수 없습니다. 이 문제는 VideoEngineView.setSecure를 try catch 절로 래핑하여 해결되었습니다.

* Zendesk #17919 - 내용 검색 시 하트비트 오류 발생첫 롤이후 검색을 시작할 때 생성된 하트비트 호출의 결과로 잘못된 입력 데이터 위치 오류가 발생했습니다. 이 문제가 해결되었습니다.

**1.4.16a** (1454a)

* Zendesk #18215 - 일부 AES 스트림을 로드할 수 없습니다.
이 문제는 AES 키를 로드하기 전에 프로필 DRM 메타데이터 크기를 확인하여 해결되었습니다.

**버전 1.4.16(1454)**

* Zendesk #3875 - Tab S CrashTVSDK가 이제 curl 대신 httpurconnection을 직접 사용하고 있으므로 CRS용 Auditude에서 OKHTTP의 종속성이 되돌려집니다. 다른 JNI 호출을 하기 전에 예외를 지워 문제가 해결되었습니다.

* Zendesk #4487 - Tracking Linear Channel of Content선형 스트림 재생 세션 동안 비디오 하트비트 추적기를 다시 초기화하도록 허용하여 문제가 해결되었습니다.

* Zendesk #17919 - Android - 컨텐츠 검색 시 하트비트 오류 발생장 내에 검색 사항이 있을 때 하트비트가 오류 상태에 있을 때의 문제가 해결되었습니다.

* Zendesk #18053 - Marshmallow에서 Adobe Primetime 충돌TVSDK가 YUV -> RGB 색상 변환을 수행하는 네온 코드를 사용하여 Android M OS에서 충돌했습니다. 이 문제는 네온이 아닌 버전의 코드를 사용하여 이 문제를 일으키는 함수를 업데이트하여 해결되었습니다.

* Zendesk #18072 - Android M - 응용 프로그램 충돌프로필 및 수준이 지원되는지 확인할 때 MediaCodecList 및 MediaCodecInfo API를 호출할 때 충돌이 발생합니다. 이 문제는 코덱이 필요한 경우에만 이러한 API를 호출할 수 있도록 미리 모든 코덱을 로드하여 임시 작업을 제공하여 해결되었습니다.

* Zendesk #18074 - Android 6.0이 있는 Nexus에서 아랍어 자막이 작동하지 않음 Android에 대한 CTS 글꼴 맵 지원을 제공하여 문제가 해결되었습니다.

**버전 1.4.15 업데이트(1438)**

* Zendesk #17437 - 일부 AES 스트림으로 VOD 컨텐츠 시작 지연 시간
이 문제를 해결하려면 매니페스트에 여러 개의 키가 나열된 경우 모든 AES 키를 동시에 다운로드하십시오.

**버전 1.4.15(1435)**

* Zendesk #4278 - ABR(적응형 비트 전송률 변경) 시 Android의 결함
최신 Android 미디어 코덱을 사용하여 매끄러운 ABR 스위치에 대한 지원을 추가하는 것이 수정되었습니다.

* Zendesk #17063 - mediaPlayer.reset()을 호출하면 비디오 엔진 재설정 오류가 발생합니다.
ErrorEvents를 전달할 때 VideoEngineExceptions의 원본 MediaErrorCode가 수정되었습니다.

* Zendesk #17130 - FireTV에서 표시되는 비트 전송률을 변경할 때 잠깐이지만 눈에 띄는 일시 중지
(위의 #4278과 동일) 최신 Android 미디어 코덱과 매끄러운 ABR 스위치에 대한 지원을 추가하는 문제가 수정되었습니다.

* Zendesk #17666 - 컨텐츠를 다시 열 때 추가 광고 마커, 예상치 않은 광고 또는 광고 없음.
VOD(Video-On-Demand) 컨텐츠를 prepareToPlay할 때 가상 시간이 아닌 로컬 시간에 초기 검색이 수행되는 문제가 수정되었습니다.

* Zendesk #17437 - 일부 AES 스트림으로 VOD 컨텐츠 시작 지연 시간
매니페스트에 여러 개의 키가 나열되면 모든 AES 키를 동시에 다운로드해야 했던 문제가 수정되었습니다.

* Zendesk #17851 - Android TV - ABRT 중 검정 프레임은 KEY_MAX_WIDTH 및 KEY_MAX_HEIGHT를 지정하여 적응형 재생을 활성화하는 것이 수정되었습니다.

**버전 1.4.14(1415)**

* Zendesk #3875 - 재생 중에 Tab S 충돌.
충돌을 방지하기 위해 추가 수정이 필요합니다.

* Zendesk #17245 - Android TV에서 폴백이 작동하지 않습니다.
폴백이 활성화되고 VMAP 응답에 빈 광고 중단이 있는 경우 재생이 중단되는 추가 문제가 해결되었습니다.

**버전 1.4.14(1412)**

* Zendesk #17245 - Android TV에서 폴백이 작동하지 않습니다.
대체 광고에서 크리에이티브 재패키징을 비활성화하기 위한 제한을 제거했습니다.

**버전 1.4.13(1388)**

* Zendesk #3502 - 광고 중단 동안 HLS 클라이언트 기반 장애 조치 지원광고 중단 기간 동안 라이브 프로필 오류가 발생할 때 주 매니페스트에 대한 장애 조치(failover)를 허용합니다.

* Zendesk #3875 - Tab S Crashes during playbackHttpUrlConnection과 cURLm 간의 충돌을 해결하려면 타사 라이브러리를 사용하십시오.

* Zendesk #4450 - 컨텐츠 해결 프로그램의 단일 배치에 대한 사용자 지정 메타 데이터 설정 문제이기회 설정에 setter를 추가합니다.

**버전 1.4.12(1388)**

* Zendesk #2751 - CSAI 및 CRS | 향상: 특정 미디어 파일 URL에서 동적 요소를 처리합니다.
동적 크리에이티브 URL을 사용하여 광고를 제대로 처리할 수 있도록 Creative Repackaging Service를 업데이트했습니다.

* Zendesk #3965 - 트릭플레이에서 일반 재생으로 전환하면 재생을 시작하기 전에 한 번 앞으로 이동합니다.
   * Fix에는 GetStreamTime을 계산하는 대신 모든 변수가 업데이트될 때까지 속도 변경 전 시간을 반환하는 TVSDK가 포함됩니다.
   * 스트림 끝 근처에 트릭 플레이 속도를 변경할 때 발생하는 충돌 문제가 해결되었습니다.
   * 트릭 플레이 중 현재 시간 계산을 수정했습니다.

* Zendesk #3978 - 8x와 16x가 자주 멈추는 트릭플레이입니다.
   * 버퍼링을 지속하지 않도록 항상 가장 낮은 비트 속도로 트릭 재생 프로필을 선택합니다.
   * 높은 트릭 플레이 속도를 위해 건너뛰기 프레임 간격을 늘릴 수 있습니다.
   * 트릭 재생 중 버퍼의 대상 길이에 도달한 후 버퍼가 계속 증가하는 문제를 해결합니다.

* Zendesk #3992 - 추가 트릭플레이 속도.
TrickPlay는 16배 이상 높은 가격을 적용하도록 업데이트되었습니다. +/- 32, +/-64 및 +/-128도 이제 허용됩니다.

* Zendesk #4007 - GEOB 개체를 타임라인 메타데이터의 일부로 해석(Android 및 웹)
setByteArray 및 getByteArray API가 추가되었습니다.

* PTPLAY-7301 - 임의 액세스 지점에서 즉시 시작
0이 아닌 시작점을 허용하도록 인스턴트 온이 업데이트되었습니다.

**버전 1.4.11(1363)**

* Zendesk #2076 - Android 4.0.3Android와 함께 Motorola Xoom에서 비디오를 재생할 때 자주 더듬거리는 소리 300개 추가 - 목록에서 이목을 끄는 컨텐츠를 재생하지 못하도록 하는 장치를 추가했습니다.

* Zendesk #2197 - `[Ads]` 추적 및 오류디스패치 OperationFailedEvent를 경고 알림과 함께 전달합니다.

* Zendesk #3304 - VAST 3.0 매크로를 `[ERRORCODE]` 채울 수 없음
   * 인라인 및 크리에이티브가 불량한 경우 오류 코드 400이 노출됩니다.
   * `[ERRORCODE]` 매크로는 URL로 인코딩됩니다.

**버전 1.4.10(1354)**

* Zendesk #2941 - 라이브 자산에 검색 가능한 범위에 &quot;0&quot;이 없습니다. 이전에는 라이브 스트림의 시작까지 검색할 때 3개의 세그먼트 버퍼가 있었으나 이제 라이브 스트림의 맨 처음 시작까지 검색할 수 있습니다(예: 첫 번째 세그먼트의 시작).

* Zendesk #3169 - Adobe Analytics 통합을 통해 참조 플레이어 업데이트 참조 플레이어가 Adobe Analytics 라이브러리로 업데이트되었습니다. 예를 들어 가져오기 기능입니다.
* Zendesk #3299 - 설명할 수 없는 트릭 플레이 동작
   * 트릭 재생을 중지한 후 재생 상태로 돌아가는 데 몇 초(때로 25초 이상)이 걸릴 수 있는 버그가 수정되었습니다.
   * 동일한 미디어에서 두 번째 트릭 재생을 호출하면 현재 시간에 스트림이 정지되는 버그가 수정되었습니다.
* Zendesk #3433 - Android 및 Flash - 자막 문제

WebVTT용 GetLine이 패킷에 대해 조정된 길이를 적용하지 않았습니다. 마지막 캡션은 이전 캡션의 문자를 포함할 수 있습니다.

* PTPLAY-6243 - 참조 플레이어를 강화하여 디버그 정보 캡처

디버그 로그를 켜고 결과를 이메일로 보내는 옵션을 사용하여 Android 샘플 참조 플레이어가 향상되었습니다. 이 옵션은 참조 플레이어의 로그 메뉴 아래에 있습니다.

**버전 1.4.9(1332)**

* Zendesk #2649 - 초기 버퍼가 꽉 찰 전에 버퍼 완료가 발생합니다.

비디오 발표자를 재생할 준비가 되기 전에 비디오 엔진이 상태를 PLAYING으로 설정하는 경우가 있습니다. 찾기 전에 버퍼 상태가 높을 때 발생합니다. 비디오 엔진에 낮은 버퍼 상태를 알려 문제를 수정했습니다. 비디오 엔진의 버퍼 상태가 낮을 경우 [재생]을 호출하면 상태가 PLAYING 대신 BUFFERING으로 변경됩니다. 상태가 PLAYING으로 변경되면 재생이 재개됩니다.

* Zendesk #2846 - 개선 사항 요청: Auditude 라이브러리에서 수행하는 호출에 대해 다른 사용자-에이전트 문자열을 설정하는 기능 제공

광고 관련 호출인 AuditudeSettings.setUserAgent(&quot;user/agent&quot;)에 대한 사용자 에이전트를 설정하기 위해 새 API가 추가되었습니다. 설정된 사용자 에이전트가 없으면 기본값이 사용됩니다. 이는 광고 관련 호출에 대한 사용자 에이전트에만 영향을 미치며 미디어 호출에 대한 사용자 에이전트는 &quot;Adobe Primetime&quot;+&lt;기본 사용자 에이전트>와 변경되지 않습니다.

**버전 1.4.8(1324)**

* Zendesk #1218 - 106000.33 로컬 오류.. 파편화된 HTTPStreamer::ThreadParseManifest()에서 매니페스트를 로드할 수 없는 경우 URL 도메인이 localhost인지 확인하고, 그렇다면 도메인을 127.0.0.1로 변경하고 ThreadParseManifest를 다시 호출합니다.
* Zendesk #3072 - 낮은 비트 전송률로 자동 전환 0PTS 페이로드를 건너뛰도록 버퍼 길이 계산을 변경했습니다.
* Zendesk #3168 - WebVTT 자막은 처음 10초 동안만 표시됩니다.
* Zendesk #3193 - TVSDK에서 프로필 변경 API 요청, PlaybackEventListener.onProfileChanged()이 추가되었습니다.

**버전 1.4.7(1311)**

* Zendesk #2197 - 추적 광고 오류 매니페스트를 로드하지 못하는 자산에 대한 알림을 추가했습니다.
* Zendesk #2575 - PSDK는 비디오 이전에 MARK 사용자 정의 스트림 광고를 무시합니다
* Zendesk #2719 - Auditude 광고를 사용한 승부, Auditude 플러그인의 상대 URL로 리디렉션될 때의 고정 비콘 추적
* Zendesk #2760 - TrickPlay 모드 동안 DISCONTINUITY 태그가 무시됩니다.
* Zendesk #2805 - 재생 시작 시 플레이어 충돌, Zendesk #2719와 동일한 수정 사항
* Zendesk #2817 - Android 플레이어 - 플레이어에서 가끔 정지 및 재생을 중단합니다. 디코드 버퍼를 2.0초에서 3.0초로 확대하여 수정됩니다.
* Zendesk #2839 - Adobe Primetime SDK가 ARMv8 칩셋을 지원합니까? Galaxy S6에서 발견된 충돌 문제 해결을 추가합니다.
* Zendesk #2885 - Auditude 충돌 재생, Zendesk #2719와 동일한 수정
* Zendesk #2895 - 10분 재생 후에도 라이브 HLS 오류가 일관되게 발생함
* Zendesk #2925 - Android 개발 빌드(1.4.5)에 대한 피드백은 패킷을 입력 대기열에 대기할 때 PTS가 음수일 경우 디코더는 이상한 상태로 전환하여 차후 패킷에 대해 음수 출력 PTS를 항상 가져옵니다. 이 문제를 방지하려면 입력 PTS가 음수이면 0으로 설정됩니다.
* PTPLAY-4645 - openssl에서 RC4 암호 지원을 끕니다. RC4의 악용 사례는 알려져 있습니다. 즉, RC4만 지원하는 서버와 연결을 시도하면 연결이 실패합니다.

**버전 1.4.6(1282)**

* Zendesk #2192 - 빠른 스위치 구현을 제거하여 네트워크 상태가 좋지 않은 경우에도 비트 전송률이 항상 낮은 것은 아닙니다.
* Zendesk #2631 - Android에서 아랍어 자막: 아랍어 글꼴의 글꼴 크기를 조정하여 여러 줄의 텍스트가 잘려 보입니다.
* Zendesk #2844 - 노트 4 및 조각 다운로드 시간의 버퍼링 시간이 정확하지 않습니다.

이 문제는 비디오 세그먼트 다운로드 간 지연을 대역폭 계산에 추가하고 다운로드 시간 계산 로직이 전체 요청 주기 시간을 사용하도록 하여 해결되었습니다.

* Zendesk #2908 - 아랍어 스크립트용 대체 글꼴 2개를 더 추가하여 Nexust 5, 6 및 7에서 아랍어 자막이 작동하지 않는 문제를 해결했습니다.
* PTPLAY-4627 - Nielson appsdk를 버전 1.2.3.7로 업데이트
* PTPLAY-5084 - 라이브 마스터 매니페스트 업데이트 장애 조치(failover) 지원

**버전 1.4.5(1248)**

* Zendesk #1757 - 일부 비디오 비트 전송률 프로필, Nexus 4 및 Nexus 7 충돌 문제가 해결되었습니다.
* Zendesk #2072 - AdEvent용 TimedMetadata에 전체 URL을 &quot;http&quot;로만 포함하지 않음
* Zendesk #2192 - 네트워크 상태가 좋지 않을 때 비트 전송률이 항상 낮은 것은 아닙니다.
* Zendesk #2256 - 마스터 재생 목록에서 구독된 태그에 대한 Metadata 이벤트를 전달하기 위해 업데이트된 PSDK인 마스터 재생 목록에 액세스합니다.
* Zendesk #2269 - WebVTT를 사용하여 화면에 두 개의 다른 자막 언어가 동시에 표시됨
* Zendesk #2417 - 플레이어에서 재생을 시작하기 전에 자막을 다운로드하려고 할 때 WebVTT에서 세그먼트 번호 일치에 잘못된 세그먼트 번호 변수를 사용하고 있었습니다. 세그먼트 색인이 0부터 시작되는 미디어에만 버그가 표시됩니다.
* Zendesk #2470 - 일시 중단 후 비트 전송률 변경이 발생하는 경우 PSDK가 일시 중단 상태에서 반환되지 않습니다. 스마트 검색이 일시 중단 상태에서 RestoreGPUResource(정지 상태에서 플레이어 복원)에 의해 호출되고 그 전에 스트림 스위치가 감지되면 스마트 검색이 완료되지 않고 지속적인 버퍼링으로 이어집니다.
* Zendesk #2451 - 자막 &#39;아래쪽 인세트&#39;, 캡션 코드에 &#39;bottomInset&#39; 매개 변수를 추가했습니다.
* Zendesk #2480 - HTTP 302 리디렉션 최적화 비활성화, useRedirectedUrl 속성 설정 지원이 추가되었습니다.
* Zendesk #2486 - 타사 비콘
* Zendesk #2547 - 아랍어 자막: 텍스트를 오른쪽으로 정렬해야 합니다.

**버전 1.4.4(1195)**

* Zendesk #1158 - Huawei Valiant에서 재생 실패(Y301A1)
* Zendesk #1709 - 미디어 크기 및 비디오 스트레치
* Zendesk #1757 - 동일한 스파/pps 데이터를 사용하여 스트림 간 프로필 전환 후 오디오만 재생됨
* Zendesk #2095 - HTTP 307 상태(리디렉션)로 인해 Adobe 플레이어가 재생을 중단합니다.
* Zendesk #2126 - 마지막 ADEVENT에 대한 TimedMetaData 이벤트 누락, 마지막 세그먼트 이후에 존재하는 구독 태그가 AVE에서 PSDK에 보고되지 않았습니다.
* Zendesk #2227 - VideoEngine의 잠금 설정 및 기본 일시 중지
* 버그 #3921755 - 버전 1.0.1L로 OpenSSL 라이브러리 업데이트

**버전 1.4.3(1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - 닫힌 캡션 켜기 및 끄기
* PTPLAY-1818 - 되감기 트릭 플레이가 광고에서 정지합니다. 지난 부분을 되감는 대신 재생합니다.
* PTPLAY-2736 - WebVTT 캡션이 포함된 스트림이 재생을 완료하면 이전에 표시된 WebVTT 캡션이 화면에 표시됩니다.
* PTPLAY-3773 - 광고 위치 후에 스트림 재생이 시작될 때 중간 롤 광고가 재생되지 않습니다.

**버전 1.4.2**

* Zendesk #1561 - Primetime에서 HLS 클라이언트 기반 장애 조치 지원 프로그램 날짜 시간을 사용하여 장애 조치 해결
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0입니다(오디오 전용으로 고정되지 않음).
* Zendesk #1626 - 플레이어의 잠재적 메모리 누수 실제 메모리 누수가 아닙니다. NotificationHistory가 지난 1000개의 알림을 저장하는 동안 문제가 발생하여 100개로 축소되었습니다.
* Zendesk #2192 - 네트워크 상태가 좋지 않을 때 비트 전송률이 항상 낮은 것은 아닙니다.

**버전 1.4.1(1121)**

* Zendesk #1951 - 4.0.x 장치에서 VideoEngine.nativeReset()의 잠금
* Zendesk #2064 - 특정 Intel 기반 Android 장치의 기본 충돌 SIGSEGV
* Zendesk #2075 - 4.0.x 장치에서 VideoEngine.nativeReleaseGPUResource참고: 이 빌드는 Android 5.0(Lollipop)을 지원하기 위해 ***필수***입니다.
* Zendesk #1513 - Android Lollipop 지원
* Zendesk #1709 - 미디어 크기 및 비디오 스트레치
* Zendesk #1871 - WebVTT 캡션이 있는 라이브 스트림을 볼 때 때때로 WebVTT 캡션이 사라지는 경우가 있습니다.
* Zendesk #1996 - PSDK 1.4.0에서 타임라인 마커가 보이지 않음
* Zendesk #2046 - PSDK 1.4.1.1113과 충돌, Auditude에서 반환되는 광고가 없을 때 실시간 스트림의 충돌 문제가 해결되었습니다.
* 버그 #3769657 - curl 버전을 7.38.0으로 업데이트
* PTPLAY-1575 - ABR 재생이 오디오 전용 스트림으로 시작한 다음 오디오/비디오 스트림으로 전환하면 오디오가 계속되는 동안 비디오가 렌더링되지 않습니다
* PTPLAY-2499 - 최신 취약점 해결을 위한 OpenSSL 버전 1.0.1j로 업데이트
* PTPLAY-2632 - Android Lollipop에서 중간 롤 광고 완료 후 비디오가 복구되지 않음
* PTPLAY-2678 - Android Lollipop에서 실시간 수명 테스트 중 비디오 가판대

**버전 1.4.0**

* Zendesk #1024 - 매니페스트를 통해 스트림에서 광고를 제거하는 기능
* Zendesk #1293 - 닫힌 캡션 트랙 선택 문제.
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0이며 mediaDuration에 올바른 값이 표시됩니다.
* Zendesk #1629 - Galaxy S4에서 광고 재생 종료 시 플레이어/앱 충돌
* Zendesk #1674 - ClosedCaption 보이지 않음, 0x03 ETX 코드가 누락된 경우 708 캡션 표시를 교정할 수 있습니다.
* PTPLAY-2157 - 스트림에서 시각적으로 다른 스타일이 설정되고 확인된 후에도 getter가 기본 자막 스타일을 반환했습니다. 이제 닫힌 캡션 스타일 속성에 설정된 값이 표시됩니다.

## 1.4의 알려진 문제 {#known-issues-in}

**버전 1.4.31**

* PTPLAY-16803 - 캡션 시스템이 작동하기 위해 비디오가 필요하므로 닫힌 캡션은 오디오 전용 컨텐츠에서 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* PTPLAY-1634 - 동일한 구독 태그의 타임스탬프가 다른 라이브 창에 있습니다. 라이브 창이 이동하는 경우 해당 기간에 있는 동일한 태그의 타임스탬프가 같아야 합니다. 하지만 같은 태그도 타임스탬프가 다른 경우가 있습니다.
* PTPLAY-3197 - 연속 재생 후 11시간 동안 Acer Iconia 디바이스에서 신호 11 SIGSEGV 오류가 발생하는 충돌
* PTPLAY-3310 - 비트 전송률이 낮은 오디오를 사용하면 Acer Iconia에서 오디오가 끊어짐/끊기가 됩니다
* PTPLAY-3355 - 연속 재생 후 4.0.x의 Motorola Xoom에서 WIN DEATH 충돌
* PTPLAY-3557 - 광고 중단에서 되감으로써 스트림이 완료됨
* PTPLAY-7079 - Android 클라이언트의 재생 창이 보안 중지/하드 정지에서 작동하지 않음
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 바뀌거나 Pulse로 나타날 수 있습니다. 자세히 관찰해야
* 버그 #3761170 - SeekToLocal in Ads with Ads는 광고 콘텐츠를 다시 검색할 수 없으므로 실시간 스트림용 currentTime API를 사용하는 것이 가장 좋습니다
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 할 때 두 개의 광고 마커가 함께 표시되는 경우가 있습니다. 이러한 광고 마커는 동일한 광고를 나타내며 한 개만 재생됩니다
* 버그 #3763373 - VOD 스트림에서 광고를 지날 때 광고 마커가 잠깐 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 부작용은 없습니다
* 일부 장치에서는 알려진 재생 문제가 있습니다. 1.4 [의 알려진 장치 문제를 참조하십시오](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 참조 구현 - 트릭 플레이가 샘플 응용 프로그램에서 구현되지 않음
* 일부 Android TV 장치에서는 다음 전환 지점에 있는 디코더 재설정으로 인해 검정 프레임을 볼 수 있습니다.
   * 트릭플레이 모드로
   * 늦게 바인딩 오디오 트랙 간 전환
   * 광고에서 기본 컨텐츠로

**버전 1.4.23**

* 캡션 시스템은 비디오가 필요하므로 닫힌 캡션은 오디오 전용 콘텐츠에서는 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* 버전 1.4.23부터 TVSDK는 Gingerbread OS 2.3을 지원하지 않습니다. 이는 TVSDK가 Gingerbread OS를 사용하는 장치에 대한 하드웨어 정보를 수집하기 위해 다음의 개인 Android 라이브러리를 사용하기 때문입니다.

   * `libstagefright.so`
   * `libcutils.so`

Android N 릴리스에서는 Google에서 이러한 비공개 라이브러리에 대한 액세스를 제거했습니다. Gingerbread OS는 현재 전 세계적으로 Android OS 시장 점유율의 1% 미만을 차지하기 때문에 버전 1.4.23이후, Gingerbread OS는 더 이상 TVSDK에서 지원되지 않을 것입니다.
버전 1.4.23(Android N 지원 포함) 이상을 사용하는 경우:
* minSdkVersion 버전 11을 사용하도록 앱을 업데이트하십시오.
* 최종 사용자가 OS 2.3을 실행 중인 경우 SDK 버전이 애플리케이션의 minSdkVersion보다 낮습니다. 시스템이 응용 프로그램의 설치 또는 업그레이드를 중단합니다.
* 최종 사용자가 OS 2.3보다 높은 버전을 실행 중인 경우 애플리케이션이 올바르게 설치됩니다.

minSdkVersion을 업데이트하는 경우:

* 최종 사용자가 OS 2.3을 실행하는 경우 애플리케이션이 설치되지만 재생은 작동하지 않습니다.
이는 업데이트 및 새로 설치할 때 모두 적용됩니다.
* 최종 사용자가 OS 2.3보다 높은 시스템을 실행 중인 경우 앱이 올바르게 설치되고 콘텐츠가 올바르게 재생됩니다.

**버전 1.4.22**

* 분할된 태그와 분할된 태그가 서로 너무 가까울 때 광고의 조기 종료는 일부 중롤 광고에서 작동하지 않습니다.

**버전 1.4.2**

* 광고 중단에서 되감으로써 스트림이 완료됩니다.

Media Player가 광고 경계에 도달할 때 트릭 플레이 되감기 작업 중 MediaPlayer Player Player State.Complete를 잘못 전송합니다. 트릭 재생 모드에서 플레이어가 이 이벤트를 무시해야 하며 그렇지 않으면 SDK에서 상태를 올바르게 처리합니다.

**버전 1.4.0(1086)**

* PTPLAY-1634 - 동일한 구독 태그의 타임스탬프가 다른 라이브 창에 있습니다. 라이브 윈도우를 이동할 때 각 파일에 있는 동일한 태그의 타임스탬프가 같아야 합니다. 하지만 같은 태그도 타임스탬프가 다른 경우가 있습니다.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE가 일시 중단에서 대체 스트림으로/여러 번 전환한 후 종종 표시됩니다.
* 버그 #3726865 - MultiBitrate LBA 스트림이 오디오 전용 스트림에서 시작하는 경우 오디오/비디오 스트림으로 전환하면 비디오가 표시되지 않습니다. 오디오/비디오 스트림에서 시작해도 이 문제가 표시되지 않으며 오디오/비디오 스트림 간을 성공적으로 전환할 수 있습니다
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 변하거나 펄스로 나타날 수 있습니다. 자세히 관찰해야
* 버그 #3761170 - 광고 포함 라이브 SEEKToLocal은 광고 콘텐츠로 되돌릴 수 없습니다. 라이브 스트림에 currentTime API를 사용하는 것이 가장 좋습니다
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 할 때 두 개의 광고 마커가 함께 표시되는 경우가 있습니다. 이러한 광고 마커는 동일한 광고를 나타내며 한 개만 재생됩니다
* 버그 #3763373 - VOD 스트림에서 광고를 지날 때 광고 마커가 잠깐 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 부작용은 없습니다
* 일부 장치에서는 알려진 재생 문제가 있습니다. 자세한 내용은 1.4 [의 알려진 장치 문제를 참조하십시오](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 참조 구현 - 트릭 플레이는 샘플 응용 프로그램에서 구현되지 않습니다.

## 1.4의 알려진 장치 문제 {#known-device-issues-in}

| 장치 | 칩셋 | 문제 | 원인 | 해결 방법 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR 지연은 디코더를 다시 시작하는 것이므로 필요합니다. |  |  |
| HTC Desire(HTC Desire HD와는 다름) | QSD8250 | 비디오를 재생할 수 없습니다. VIDEO_PROFILE_NOT_SUPPORTED 오류를 반환합니다. | 욕망은 적절한 HW 디코더를 제공하지 않습니다. Stageright의 SW 디코더를 제공합니다. | 장치를 다시 시작합니다. |
| HTC EVO 4G | QSD8650 | HW 디코더가 없습니다. | Qualcomm에는 HW 디코더가 없습니다. | Android 4.x로 업그레이드 |
| Kindle FireSystem 버전 6.0 | TI OMAP4 | HLS 스트림을 재생하지 않습니다. AIR에서 비디오가 작동하지 않습니다. |  | 시스템 버전 6.3으로 업그레이드 |
| Kindle Fire HD | TI OMAP4 | 비디오를 재생할 수 없는 상태로 전환할 수 있습니다. VIDEO_PROFILE_NOT_SUPPORTED 및 UNRECOVERABLE_ERROR 오류를 반환합니다. | HW 디코더는 앱에서 HW 디코더가 완전히 종료되지 않는 경우(예: 충돌 발생 후) 복구할 수 없는 상태로 전환됩니다. 장치의 기본 앱에서도 발생합니다. | 장치를 다시 시작합니다. |
| Kindle Fire HD 8.9 | Snapdragon 800 | 여러 ABR 스위치 후에 AVE 충돌이 발생했습니다. |  |  |
| Motorola Atrix | Tegra2 | AIR가 아닌 AVE와 관련된 전반적인 성능 문제 오디오/비디오가 동기화되지 않은 경우 비디오 재생이 9분에서 15분 사이에 끝난 후에 멈춥니다. 충돌. | AIR에서 활성화되는 openGLES와 관련되었을 수 있습니다. 조사 중입니다. |  |
| Nexus 7(2세대) | S4Pro APQ8064 (Qualcomm) | 동영상을 30분 이상 일시 중지하면 장치가 정지됩니다. | Google에 보고된 장치 문제. | 긴 일시 중지 상태를 허용하지 않도록 앱이 시간 초과되어야 합니다. |
| Nexus S(GB) | 허밍 버드 | HW 디코더를 사용하여 비디오를 재생할 수 없습니다. | Nexus S에는 Stageright 기반 HW 디코더가 없으므로 Android 2.3에서는 SW 디코더를 사용하고 있습니다. | ICS로 업그레이드 |
| Nexus S(ICS) | 허밍 버드 | 비디오가 깜박이는 경우도 있습니다. | 데이터가 잘못되면 디코더가 잘못된 상태로 전환될 수 있습니다. | 장치를 다시 시작합니다. |
| Nook tabletAndroid OS: 2.3 | TI OMAP 4 | 비디오가 재생되지 않고 앱이 멈춥니다. | Stagefright는 앱을 몇 번 실행한 후 불안정한 상태로 전환됩니다. mediaplayer::QueryCodecs를 호출합니다. | 장치를 다시 시작하여 상태를 재설정합니다. |
| 삼성 갤럭시 ACE | Qualcomm MSM7227 | SampleMediaPlayer 앱을 설치할 수 없습니다. | 더 일반적인 ARM v7 칩셋 대신 ARM v6을 사용합니다. FP/AIR는 이 장치를 지원하지 않습니다. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | 비디오를 재생할 수 없습니다. | 이 칩셋은 AVE의 Android 사전 ICS용 알 수 없는 디코더입니다. |  |
| Samsung Galaxy S2(GT-I9100) | Exynos | 비디오 성능이 이 장치에 적합한 것은 아닙니다. | HW 디코더가 잘못된 PTS로 디코딩된 프레임을 반환합니다. 디코더가 프레젠테이션 시간 대신 디코딩 시간을 사용하고 있는 것 같습니다. |  |
| 삼성 갤럭시 S2 GAandroid OS: 2.3.6 | TI OMAP4 | 비디오를 시작할 때 충돌이 발생합니다. |  | Android 2.3.7 또는 4.x로 업그레이드 |
| Samsung Galaxy S3(I747) | Qualcomm MSM8960 | 간헐적으로 비디오가 중지되고 오디오만 재생되면 응답하지 않습니다. |  |  |
| 삼성 갤럭시 S3 I747M | SAMSUNG_M2ATT | 비디오가 멈춥니다. | 조사 중. |  |
| 삼성 갤럭시탭 1 v10.1 | Tegra 2 | MBR 전환에는 최대 3초가 걸릴 수 있습니다. | MBR 충돌을 해결하기 위해 최대 3초가 걸릴 수 있는 모든 스트림 스위치에 대한 디코더를 다시 시작합니다. |  |
| 삼성 갤럭시 Y |  | SampleMediaPlayer 앱을 설치할 수 없습니다. | 더 일반적인 ARM v7 칩셋 대신 ARM v6을 사용합니다. FP/AIR는 이 장치를 지원하지 않습니다. |  |
| Xoom | 테그라 | 전환하는 데 필요한 프레임을 몇 개 놓습니다. 디코더가 다시 시작되지 않습니다. | OMXAL 제한. |  |

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 페이지에서 [전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.
