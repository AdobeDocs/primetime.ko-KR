---
title: Android용 TVSDK 1.4 릴리스 노트
description: Android용 TVSDK 1.4 릴리스 노트에서는 TVSDK Android 1.4의 새로운 기능 또는 변경 사항, 해결된 문제 및 알려진 문제, 장치 문제에 대해 설명합니다.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# Android용 TVSDK 1.4 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 1.4 릴리스 노트에서는 TVSDK Android 1.4의 새로운 기능 또는 변경 사항, 해결된 문제 및 알려진 문제, 장치 문제에 대해 설명합니다.

## 새로운 기능 {#new-features}

**버전 1.4.43**

**HTTPS를 통한 보안 광고 로드**

Adobe Primetime은 HTTPS를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

**MediaPlayer 클래스의 alwaysUseAudioOutputLatency(boolean val)**

이 매개 변수가 설정되면 오디오 타임스탬프 계산에서 오디오 출력 지연 시간을 사용합니다.

부울 매개 변수 val을 허용합니다. 값이 인 경우 `True`, 클라이언트는 오디오 타임스탬프 계산에서 오디오 출력 지연 을 사용합니다.

**버전 1.4.42**

**부분 광고 브레이크 삽입:**
부분적으로 시청한 광고에 대한 추적을 실행하지 않고 광고 중간에 참여하는 TV와 같은 경험.
예: 사용자가 3개의 30초 광고로 구성된 90초 광고 브레이크 중간(40초)에 참가합니다. 중간 광고 두 번째 광고에 10초입니다.
* 두 번째 광고가 나머지 기간(20초) 동안 재생되고 세 번째 광고가 재생됩니다.
* 재생되는 부분 광고(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고의 추적기만이 발사된다.

**버전 1.4.41**

새 기능이 없습니다.

**버전 1.4.40**

새 기능이 없습니다.

>[!NOTE]
>
>1.4.39 이전 버전을 사용하는 경우에는 API를 변경할 필요가 없습니다.

**버전 1.4.39**

* TVSDK는 VHL 2.0.1과 VHL 2.0.1에서 Nielsen으로 인증됩니다.
* Android TVSDK가 새 Akamai 호스트에서 CRS 요청을 수행하도록 업데이트되었습니다 `primetime-a.akamaihd.net`.
* 새 호스트 이름 구성은 HTTP와 HTTPS(SSL) 모두를 통해 더 큰 규모로 CRS 자산 전달을 제공합니다.
* TVSDK는 Android Oreo 릴리스를 지원합니다.
* 새 함수가에 추가됩니다. `AdClientFactory` 여러 Opportunity Detectors 등록을 지원하는 클래스:

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  이 경우 PlacementOpportunityDetector 배열이 반환됩니다. 이제 여러 Opportunity Detectors 를 등록할 수 있습니다. 예를 들어 조기 광고 종료 기능의 경우 두 개의 Opportunity Detectors 가 필요합니다. 하나는 광고 삽입용 이고 다른 하나는 광고의 조기 종료용 입니다. 이 새 함수는 자체 AdvertisingFactory를 구현한 경우(DefaultAdvertisingfactory를 사용하지 않는 경우)에만 영향을 줍니다. 기존 동작을 가져오려면 createOpportunityDetector() 함수에서와 같이 단일 Opportunity Detector를 만들고 배열에 넣은 다음 반환해야 합니다.

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
>1.4.39 이전 버전을 사용하는 경우에는 API를 변경할 필요가 없습니다.

**버전 1.4.36**

Android에서 콘텐츠 건너뛰기에 대한 버그 수정.

**버전 1.4.35**

* **네트워크 광고 정보**

  이제 TVSDK API는 서드파티 VAST 응답에 대한 추가 정보를 제공합니다. 광고 ID, 광고 시스템 및 VAST 광고 확장은 광고 자산의 networkAdInfo 속성을 통해 액세스할 수 있는 NetworkAdInfo 클래스에 제공됩니다. 이 정보는 와 같은 다른 Ad Analytics 플랫폼과 통합하는 데 사용할 수 있습니다. **모트 분석**.

**버전 1.4.31**

**CRS 광고에 대한 다중 CDN 지원**
* 기본적으로, 트랜스코딩된 모든 자산은 Akamai의 Adobe 소유 CDN에서 호스팅됩니다. 최신 릴리스에서는 CRS(Adobe Creative Repackaging Service)를 통해 고객이 지정한 대로 여러 CDN에 트랜스코딩된 크리에이티브를 업로드할 수 있습니다.
* 기본 URL이 사용되지 않을 때 최종 CRS 크리에이티브 URL을 지정할 수 있도록 새 API가 TVSDK에 추가됩니다. 이러한 새로운 API를 사용하는 방법은 설명서를 참조하십시오.

**버전 1.4.18**
이제 Primetime Android TVSDK는 VPAID 2.0 Javascript 크리에이티브를 지원하여 풍부한 대화형 스트림 내 광고 경험을 활성화할 수 있습니다. VPAID 2.0에 대한 자세한 내용은 [VPAID 광고 지원](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**버전 1.4.17**

AC-3 5.1은 Amazon FireTV에서만 지원됩니다.

**버전 1.4.11**

* **광고 대체, 광고 선택 로직의 데이지 체인(Zendesk #3103** 대체 규칙이 활성화된 VAST 광고(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 대체 광고를 사용하려고 시도합니다. 대체 동작의 몇 가지 측면을 구성할 수 있습니다.

자세한 내용은 [VAST 및 VMAP 광고에 대한 광고 대체](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **비디오 하트비트 라이브러리(VHL)가 버전 1.5로 업데이트되었습니다**
   * 비디오 시작 및/또는 비디오/광고/챕터 시작을 컨텍스트 데이터로 사용하여 메타데이터를 전송하는 기능
   * 네트워크 트래픽 감소 - 하트비트가 평균적으로 더 적고 크기가 더 작습니다.

**버전 1.4.7**

* **On-Premise 개인화 지원**&#x200B;다른 엔드포인트로 이동하도록 클라이언트의 개별화 요청을 맞춤화하기 위해 Adobe 개별화 서버의 온-프레미스 설치를 지원합니다.

**버전 1.4.6**

* **샘플 AES 암호화(Flash Player 버전 17.0.0.134 필요)**이제 샘플 기반 AES 암호화가 지원됩니다.

**버전 1.4.2**

* **비디오 하트비트 라이브러리(VHL)가 버전 1.4.0.1로 업데이트되었습니다**

   * Adobe Analytics Video Essentials를 사용하여 다른 SDK 또는 플레이어의 다양한 분석 사용 사례를 번들로 제공하는 기능이 추가되었습니다.
   * 광고 추적은 trackAdBreakStart 및 trackAdBreakComplete 메서드를 제거하여 최적화되었습니다. 광고 브레이크는 trackAdStart 및 trackAdComplete 메서드 호출에서 추론됩니다.
   * 광고를 추적할 때 플레이헤드 속성이 더 이상 필요하지 않습니다.

* **Nielsen SDK 통합**&#x200B;이제 TVSDK는 사용자 지정 통합 없이 Nielsen SDK에 사용자 추적 정보 전송을 지원합니다.

**버전 1.4.0**

* **대체 컨텐츠 대체와 함께 일시 중단 신호** 1.4 TVSDK 업데이트의 일부로, 이제 TVSDK는 선형 콘텐츠에 대한 지역 일시 중단에서 시작 및 반환을 지원합니다. 이제 TVSDK는 원본 프로그래밍 대신 대체 프로그래밍이 표시되고 있는 경우에도 블랙아웃 신호를 모니터링하기 위해 주 매니페스트 파일과 대체 매니페스트 파일을 나란히 처리할 수 있습니다.

* **C3 광고 제거/바꾸기** 이제 C3 창에서 나오는 VOD(Video-on-Demand) 자산에 새 광고를 동적으로 삽입하기 위해 추가 준비 작업이 필요하지 않습니다. 이제 TVSDK에서 사용자 지정 콘텐츠 범위를 제거하고 새 광고를 동적으로 삽입하기 위한 API를 제공합니다. 이 강력한 새 기능은 라이브/선형 컨텐츠가 브로드캐스트 중에 방송되고 자산을 &quot;정리&quot;할 적절한 시간 없이 온디맨드 컨텐츠로 사용하기 위해 즉시 풀다운되는 경우에도 유용합니다.

* PlaybackEventListener 인터페이스에는 새 이벤트를 수신하는 데 사용할 수 있는 onReplaceMediaPlayerItem이라는 새 메서드가 있습니다. `ITEM_REPLACED`. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스가 대체될 때마다 발송됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.
* AdClientFactory에는 여러 Opportunity Detectors에 등록할 수 있도록 클래스에 새로운 기능이 추가되었습니다.

  ```
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
  
  For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
  
  To override this new function create a single Opportunity Detector, and put into an array and return:
  
  @Override
  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
  
  return opportunityDetectors;
  }
  
  }
  ```

## 1.4에 대한 TVSDK 변경 사항 {#tvsdk-changes}

* PlaybackEventListener 인터페이스에는 onReplaceMediaPlayerItem이라는 새 메서드가 있습니다. 이 메서드는 새 이벤트인 ITEM_REPLACED를 수신하는 데 사용할 수 있습니다. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스가 대체될 때마다 발송됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.

* AdClientFactory에는 여러 Opportunity Detectors에 등록할 수 있도록 클래스에 새로운 기능이 추가되었습니다.

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

예를 들어 조기 광고 종료 기능의 경우 두 개의 Opportunity Detectors 가 필요합니다. 하나는 광고 삽입용 이고 다른 하나는 광고의 조기 종료용 입니다.

이 새 함수를 재정의하려면 단일 Opportunity Detector 를 만들고 배열에 넣은 다음 를 반환합니다.

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4의 장치 인증 및 지원 {#device-certification-and-support-in}

>[!NOTE]
>
>다음 기능은 다음과 같습니다 **아님** tvsdk에서 지원됩니다.
>
>* 플랫폼 또는 버전에서 슬로우 모션.
>* 라이브 트릭 플레이.

**버전 1.4.43**

TVSDK 1.4.43은 Android 6.0.1/ 7.0 및 8.1(Oreo)이 있는 Android 장치로 인증되었습니다.

* **버전 1.4.23:**

   * TVSDK 1.4.23은 Android N이 있는 Android 장치에 대해 인증되었습니다.

* **버전 1.4.18:**

   * Primetime은 Amazon Fire TV 인증을 받았습니다.
   * VPAID 2.0은 Android 4.0 이상이 설치된 장치에서만 지원됩니다.

## 1.4에서 해결된 문제 {#resolved-issues-in}

>[!NOTE]
>
>CRS를 사용하는 모든 TVSDK 고객은 iOS 및 Android에서 TVSDK 1.4.39 또는 최신 버전으로 업그레이드하는 것이 좋습니다. 이 업그레이드는 기존 앱 구현에 대한 드롭인 대체입니다. 업그레이드 후 프록시 도구(예: Charles)에서 CRS 크리에이티브 URL 요청을 확인하여 경로의 버전이 버전 3.1을 반영하는지 확인합니다. 예:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**버전 1.4.43**

* 티켓 #27143 - FireTV 장치에서 5.1 오디오 트랙을 재생할 수 없음

   * 이제 TVSDK에서 FireTV 장치에서 AC3 오디오를 재생할 수 있습니다. 재생은 항상 스테레오입니다.

* 티켓 #33902 - HTTPS를 통한 보안 광고 게재

   * Adobe Primetime은 https를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

* 티켓 #34493 - Bluetooth 오디오 지연

   * 추가됨 `alwaysUseAudioOutputLatency` 설정할 때 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용하는 MediaPlayer 클래스입니다.

* Ticket #34949 - 비디오 하트비트 라이브러리(VHL)의 새 버전이 통합되었습니다.

**버전 1.4.42(1791)**

* Zendesk #33719: FireTV 4k 적응형 비트율 확장이 느립니다. FireTV 4K 장치용 ABR에 대한 지원이 추가되었습니다.
* Zendesk #33338: resetDRM은 애플리케이션의 모든 데이터를 지웁니다.  TVSDK가 아닌 스레드의 예외로 인해 TVSDK 작업 큐가 꽉 차는 추가 사례를 처리했습니다.

**버전 1.4.41(1776)**

* Zendesk #33002 - Fire TV에서 TVSDK의 컴패니언 에셋 데이터. Companion 데이터를 List로 반환하는 새 클래스 AdBannerAsset를 구현했습니다. &lt;adbannerasset> 및 AdAsset::id가 이제 Long이 아닌 String입니다.
* Zendesk #32821 - Android Primetime 플레이어가 WWE용 프레젠테이션 타임스탬프(PTS)를 만나면 중지됩니다. 이 문제는 이 릴리스에서 해결되었습니다.
* Zendesk #33572 - VideoAnalyticsProvider 광고 시작 충돌. VideoHeartbeat.jar의 VHL+Nielsen 공동 SDK 버전의 올바른 조합을 사용하여 이 문제를 해결했습니다.
* Zendesk #33355 - 화재 TV: 15 초 문제를 다시 스크러빙. TVSDK측과 고객은 최종 및 서드파티에서 이를 확인하고 수정 사항이 없습니다.

**버전 1.4.40(1764)**

* Zendesk #33068 - 새 장치에서 Amazon 립 동기화 문제. Lip 동기화 문제는 이 릴리스에서 수정되었습니다.
* Zendesk #32215 - Android TVSDK 1.4.38 보안 문제 `[Hotlist]`. 최신 OpenSSL-1.1.0 및 curl-7.55.1로 업데이트되었습니다.
* Zendesk #32920 - 광고 브레이크 내에 빈 화면이 있고 광고 브레이크 완료가 없습니다. VPAID 컨테이너가 중단 상태로 전환되는 문제를 해결하고 Facebook VPAID 광고가 종종 단일 \&amp;lt;AdParameters\&amp;gt; VAST 노드에 있는 여러 CDATA 블록을 반환하는 문제를 해결했습니다.

**버전 1.4.39(1744)**

* Zendesk #28976 - 라이선스 요청이 1초 이상 소요됩니다. POST을 사용하는 DRM 라이센스 요청 호출이 실행되는 동안 Curl은 &quot;Expect: 100-continue&quot; 헤더를 추가합니다. TVSDK에서 &quot;Expect:&quot; 헤더가 제거되었습니다.
* Zendesk #27707 - CSAI 환경이 조기 반환 또는 콘텐츠 반환을 위한 CUE IN 마커를 준수하지 않습니다. 여러 영업 기회 생성기를 지원합니다.

**버전 1.4.38 (1722)**

* Zendesk #21590 - 최신 원본 빌드의 비디오 성능 및 추적

API의 복잡성을 줄여 VideoHeartbeatsLibrary 구현의 장벽을 줄이기 위해 TVSDK에서 VHL 2.0을 통합하고 인증합니다.

* Zendesk #29688 - Android O Beta 고객 지원.

새 Android 베타 릴리스에 대한 TVSDK 지원.

**버전 1.4.36 (1713)**

* Zendesk #27392 - Android에서 콘텐츠 건너뛰기

암호 해독을 수용하기 위해 Android TVSDK가 iframe 이외의 콘텐츠의 바이트 범위를 16바이트로 잘못 확장했습니다. Iframe 스트림의 경우 확장이 필요하지만 비 iframe 스트림의 경우에는 그렇지 않습니다.

**버전 1.4.34 (1702)**

* Zendesk #27638 - cURL INet 개체에서 누수

Posix cURL INet 개체가 cURL 연결에 사용된 공유 관리자 및 DNS 캐시를 보유하는 동안 누출되었습니다.

이 문제는 INet 해체기에서 Posix cURL INet 개체를 삭제하여 해결했습니다.

**버전 1.4.33(1694)**

* **OpenSSL 라이브러리**

OpenSSL 라이브러리가 OpenSSL 버전 1.0.2j로 업데이트되었습니다.

* Zendesk #21701 - 표준화된 URL 대신 1401 CRS 요청에 대한 원래 크리에이티브 URL을 전송합니다.
이 문제는 원래 크리에이티브 URL을 전송하여 해결됩니다.

* Zendesk #25023 - 비디오 재생 시간이 오래 걸림, 화면이 깜박임 CenturyLink 셋톱 박스 장치에 대한 최대 비디오 형식 차원을 설정하여 이 문제를 해결했습니다.

* Zendesk #27460 - 새 Akamai 계정이 POST cdn 요청을 처리할 수 없습니다.
코드를 업데이트하여 `cdn.auditude.com` POST 대신 GET이 되도록 요청합니다.

* Zendesk #28245 - 앱이 배경에서 전경으로 이동할 때 재생 상태가 올바로 통지되지 않음 이 문제는 애플리케이션이 전경으로 돌아갈 때 재생 상태를 재생 또는 일시 중지로 올바로 복원함으로써 해결되었습니다.

**버전 1.4.32(1682)**

* Zendesk #25779 - TVSDK Android 4.2 이하에서의 보안 취약점에는 WebView에서 JavaScript가 활성화되어 있을 때 보안 취약점이 있습니다. OS 4.2 이하를 실행하는 장치에서 TVSDK에서 WebView를 사용할 수 없습니다. 이렇게 하면 해당 장치에서 TVSDK의 VPAID 광고 사용이 비활성화됩니다.

* Zendesk #26890 - 화면 내 문제(ON/OFF) 처리 참조. 플레이어 Adobe 비디오 엔진(AVE)이 일시 중단된 상태에서 다시 시작될 때 DefaultMediaPlayer가 상태를 업데이트하지 않습니다. 따라서 AVE가 재생 상태에 있더라도 DefaultMediaPlayer는 SUSPENDED 상태로 유지됩니다. 이 문제는 DefaultMediaPlayer의 현재 상태가 일시 중지된 경우에도 AVE에서 재생 상태를 수신할 때 DefaultMediaPlayer 상태를 재생으로 설정하여 해결되었습니다.

**버전 1.4.31(1675)**

* Zendesk #21974 - null 오브젝트로 인한 예외
   * AdIndex는 null일 때 거의 증가하지 않습니다. 프리롤 adBreak에 대해 수신된 잘못된 API 호출 때문일 수 있습니다. 이러한 예외를 방지하기 위해 데이터 유형을 수정했습니다

* Zendesk #24714 - 외부 로깅 끄기
   * 관련 없는 로깅을 해제하도록 TVSDK를 업데이트했습니다.

* Zendesk #24488 - Fire TV의 AV 동기화 문제
   * AV 디코더 스레드 처리를 개선하여 해결되었습니다. 특히, 입력 또는 출력 프레임 큐들이 수정될 때마다, 프레임의 콘텐츠 유형에 특정된 디코더 스레드가 실행된다.

* Zendesk #26551 - CRS 오류 수정
   * 요청이 HEAD(http head)인 경우 비어 있으므로 콘텐츠를 읽을 필요가 없습니다. 읽어봐도 좋지만 read()를 호출하는 동안 이전 Android(4.0.x)가 중지되고 read()를 호출하는 경우 최신 Android가 올바른 값(-1)을 반환합니다. 이에 따라 는 &quot;head&quot;에 대한 콘텐츠를 읽지 않도록 코드를 변경했습니다.

* TrickPlayManager에 액세스할 때 Zendesk #26696 Null 포인터 예외가 발생합니다.
   * 사용하기 전에 TrickPlayManager 개체가 null이 아닌지 확인하여 수정했습니다.

**버전 1.4.30(1659)**

* Zendesk #22675 에셋 기간이 라이브/선형 스트림에 대해 업데이트되지 않음 이 문제는 라이브 및 선형 스트림에 대한 에셋 기간을 제공하는 PTVideoAnalyticsTrackingMetadata에 새 API인 assetDuration을 제공하여 해결되었습니다.

* Zendesk #25853 채널 전환 시 TVSDK의 메모리 누수 MediaPlayer가 재설정되거나 파일을 다운로드하는 동안 릴리스될 때 파일 읽기 버퍼 누수가 발생하는 문제가 해결되었습니다.

**버전 1.4.29(1653)**

* Zendesk #21200 - 앱이 백그라운드에 있을 때 플레이어가 일시 중단 상태에서 복구되지 않음 스트림 전환 신호를 받은 후 플레이어가 일시 중단되었을 때 이전 위치로 복원하는 대신 일시 중단 상태에서 플레이어를 복원할 때 플레이어가 스트림 전환을 수행할 수 있습니다.

* Zendesk #23412 - 광고 브레이크의 마지막 3초 내에 광고를 클릭할 경우 플레이어가 블랙박스와 함께 고정됩니다. 이 문제는 Zendesk #21200과 동일한 문제입니다.

* Zendesk #23616 - 건너뛴 광고 브레이크가 너무 먼 미래에 검색됨 광고 삽입 유형(삽입/바꾸기)에 따라 TVSDK는 광고 브레이크 끝점을 결정하기 위해 광고 기간을 계산에 사용할지 여부를 결정합니다.

* Zendesk #25078 - Android TV STB의 TVSDK DRM 메모리 누수 DRM 어댑터 개체에 대한 메모리 누수가 검색 및 수정되었습니다.

* Zendesk #25067 - VideoEngineTimeline의 충돌 이 문제는 개체가 올바르게 정리되지 않고 개체가 소멸된 후 이벤트가 호출되어 발생합니다. null 예외를 방지하기 위한 검사를 추가하여 문제가 해결되었습니다.

* Zendesk #25352 - 사용자 지정 HTTP 헤더 설정 이 문제는 TVSDK의 허용 목록에 새 사용자 지정 헤더를 추가하여 해결되었습니다.

* Zendesk #25617 - 라이브 스트림 PTS 롤오버로 플레이어 불연속 및 메모리 충돌 발생 이 문제는 세그먼트 중간에 롤오버가 발생할 때 FragmentedHTTPStreamer에서 PTS 롤오버 처리를 추가하여 해결되었습니다.

**버전 1.4.28 (1637)**

* Zendesk #23618 - 광고 정책이 참조되기 전에 광고 브레이크 이벤트가 실행됨 광고가 adForgery로 인해 건너뛸 때 AD_BREAK_START 및 AD_START 이벤트가 실행되지 않음으로써 이 문제가 해결되었습니다. 대신 AD_BREAK_SKIPPED 이벤트가 전송됩니다.

**버전 1.4.27 (1631)**

* Zendesk #23174 - 비디오 크기를 조정할 때 발생하는 성능 문제 TVSDK가 MediaPlayerView에서 SurfaceHolder.setFixedSize()에 액세스할 수 있도록 해주는 새로운 API인 MediaPlayerView.setSurfaceFixedSize를 증명하여 이 문제를 해결했습니다.

* Zendesk #24450 - TVSDK에서 중복 광고 요청을 수행함 이 문제는 경과 시간이 두 배가 아닌 long으로 변환되었을 때 발생했으며, 이 문제를 수정했습니다.

**버전 1.4.26 (1627)**

* Zendesk #21436 - OpenSSL 라이브러리가 버전 1.0.2h로 업데이트 OpenSSL 라이브러리가 OpenSSL 버전 1.0.2h로 업데이트됨
* Zendesk #23825 - Android 쿠키에 대한 지원을 제공하여 수정된 콜백에 쿠키가 포함되지 않습니다.

**버전 1.4.25 (1620)**

* Zendesk #22900 - 라이브 Adobe Primetime DRM 스트림이 Android 참조 플레이어에서 재생되지 않습니다. 메모리 할당 문제가 해결되었습니다.
* Zendesk #23176 - VPAID 광고를 재생하려고 할 때 애플리케이션이 충돌합니다. 애플리케이션이 VPAID 광고를 렌더링하는 사용자 지정 광고 보기를 만들지 않았기 때문에 충돌이 발생했습니다. 이 문제는 사용자 지정 광고 보기가 없는 경우 광고 서버 응답에서 VPAID 광고를 무시하여 해결되었습니다.

* Zendesk #23153 - SampleAES DRM 스트림 - TVSDK 참조 플레이어의 재생 중단 이 문제는 Zendesk #22900과 동일합니다.

**버전 1.4.24 (1612)**

* Zendesk #20784 - Analytics: 라이브 비디오 전환에 대한 콘텐츠 완료 트리거 이 문제는 라이브/선형 비디오 추적 세션 중에 콘텐츠 완료를 수동으로 트리거하기 위한 API(trackVideoComplete)를 추가하여 해결되었습니다.

* Zendesk #21977 placeAdBreak/acceptAd 작업 중 VideoEngineTimeline 충돌
   * 이 문제에서 다음 라이브러리가 업데이트되었습니다.
      * AdobeMobile 라이브러리를 버전 4.10.0으로
      * VHL 라이브러리에서 버전 1.5.6으로
      * VHL-Nielsen 라이브러리에서 버전 1.6.7로

이 문제는 광고를 허용된 광고 목록에 추가하기 전에 null 검사를 추가하여 해결되었습니다.

* Zendesk #22313 Amilogic 칩셋이 있는 STB의 비트율이 1.2M를 넘지 않습니다. 미디어 코덱 기능을 미리 로드하고 Amilogic 칩셋 장치에 대한 원활한 스위치를 비활성화하여 이 문제를 해결했습니다.

* Zendesk #19520 샘플 AES HLS 자산이 TVSDK 플레이어에서 재생되지 않음 샘플 AES 암호화 HLS 스트림에 대한 여러 PMT 설명자를 처리하여 이 문제를 해결했습니다.

**버전 1.4.23 (1602)**

* Zendesk #18852 - CRS 규칙을 기반으로 크리에이티브 선택 논리 업데이트 이 문제는 크리에이티브 선택 우선 순위를 지정하기 위해 JSON 구성 파일을 추가하여 해결되었습니다.

* Zendesk #20861 - Android N 이 릴리스는 Android N에서 실행되는 애플리케이션에서 더 이상 액세스할 수 없는 Android 플랫폼 기본 라이브러리를 직접 사용하는 기능을 제거하여 Android N을 지원합니다.

* Zendesk #21018 - Android N 충돌 ZD# 20861과 동일한 해상도.

* Zendesk #21266 - Invalid_Key 오류에서 VideoEngineAdapter가 충돌합니다. Invalid_Key 오류에는 AVE의 설명이 포함되지 않으므로 텍스트를 구문 분석하면 NPE가 발생합니다. 설명을 구문 분석하기 전에 onError 중에 설명에 대한 null 검사를 추가하여 문제를 해결했습니다.

* Zendesk #22286 - 기본 라이브러리가 메모리 읽기 키/조각 할당을 통해 충돌을 일으킵니다. 여러 키가 있는 매니페스트를 동시에 로드하려고 할 때 Android에서 발생한 이 충돌이 수정되었습니다.

**버전 1.4.22 (1581)**

* Zendesk #17236 - DRM이 있는 HLS 비디오의 재생 헤드 시간을 신뢰할 수 없음 오디오 세그먼트 시작 시간이 비디오 세그먼트 시작 시간과 일치하지 않는 LBA 스트림으로 시간 이동이 수정되었습니다.

* Zendesk #17680 - 비디오 재생이 Selevision Andredo 상자에서 중지됩니다. 이 장치의 비디오 디코더는 출력 버퍼에서 비디오 프레임을 대기열에서 뺄 때 상당한 출력 시간 점프를 반환하며 이 출력 타임스탬프는 높게 유지됩니다. 이 문제는 을(를) 반환하여 해결되었습니다. *비디오 프로필이 지원되지 않음* 플레이어가 동일한 프로필을 다시 시도하거나 다른 프로필을 선택하게 하지 않는 오류입니다.

* Zendesk #19074 - FFWD 및 REW 트릭 플레이 중 비디오 고정 이 문제는 트리크플레이가 종료되었으며 복구할 수 없는 오류로 인해 비디오가 일시 중지되었음을 응용 프로그램에 알리는 새 경고 TRICKPLAY_ENDED_DUE_TO_ERROR를 추가하여 해결되었습니다.

* Zendesk #19574 - TVSDK가 DRM 또는 비 DRM 콘텐츠에 대한 M3U8 응답 데이터를 반환하지 않습니다. 이 문제는 다음과 같은 방법으로 해결되었습니다.

* Zendesk #19986 - Android TV와 같은 특정 장치에서 손상된 OP 동작
* FILE_NOT_FOUND 오류를 조건에 추가합니다.
* 다음 위치에서 오류가 발생하는 경우: *파일을 찾을 수 없음* 오류. 응답을 사용할 수 있는 경우 오류 설명에서 URL 및 응답을 구분합니다.
NVidia 실드 OP 지원으로 인해 발생한 논리 오류가 해결되었습니다. NVidia가 아닌 장치에서는 표시 유형을 알 수 없는 경우에도 표시 보안 플래그를 신뢰합니다.

* Zendesk #20549 - 오래된 플레이리스트 처리. 이 문제는 이전 가져오기에서 새 세그먼트를 받지 못하는 경우 라이브 매니페스트 업데이트 간격을 예상 세그먼트 기간의 절반으로 줄임으로써 해결되었습니다.

* Zendesk #20742 - FireTV에서 라이브 콘텐츠를 재생할 때 메모리 사용량이 계속 증가하는 것으로 나타납니다. 충돌은 한도에 도달한 JNI 개체 참조 테이블로 인해 발생합니다. 디코더를 다시 시작할 때 만든 MediaFormat 개체에 대한 참조를 삭제하여 이 문제를 해결했습니다.

* Zendesk #21125 - 라이브/선형 광고 브레이크에서 조기 반환(CSAI). 플레이어가 opportunity detector에서 splice를 사용하여 광고 큐에서 스플라이스를 등록하는 경우 광고 브레이크 중에 플레이어가 기본 컨텐츠로 돌아갈 수 있는 기능이 추가되었습니다.

* Zendesk #21334 - 서드파티 광고 요청에 대한 TVSDK 광고 요청 시간 초과 값입니다. 광고 호출에 대한 전역 시간 제한을 활성화하는 adRequestTimeout 설정이 AdvertisingMetadata에 추가되었습니다.

**버전 1.4.21(1566)**

* Zendesk #17781 - ADB screencapture가 더 이상 작동하지 않음 이 문제는 화면 캡처를 허용하는 DefaultMediaPlayer.create(Context context context, boolean secureSurface) API를 추가하여 해결되었습니다.
화면 캡처를 허용하려면 secureSurface에 대해 false를 전달합니다.
중요: 프로덕션 설정에서는 이 화면 캡처 기능을 활성화하지 않는 것이 좋습니다.

* Zendesk #19074 - FFWD 및 REW 트릭 플레이 중 비디오 고정 TrickPlay가 플레이백에서 동결될 수 있을 때 발생한 다음 문제가 해결되었습니다.

* Zendesk #19532 - 닫힌 캡션이 잘못된 순서로 표시됨
   * FHS는 트리크플레이를 시작하지만 첫 번째 iframe 세그먼트에는 프레임이 없습니다.
   * iframe 세그먼트를 다운로드하는 동안 FHS가 오류 조건에 도달하면 trickplay에서 종료되고 재생이 일시 중지됩니다.
   * Andorid MediaCodec 구현은 모든 입력/출력 버퍼를 플러시하라는 메시지가 표시되는 동안 입력 큐 가용성을 계속 기다립니다.
이 문제는 WebVTT 큐의 순서를 반대로 하여 여러 겹치는 큐가 &quot;위로 스크롤&quot;하는 것처럼 보이도록 하여 해결되었습니다.

* Zendesk #19574 - TVSDK가 DRM 또는 비 DRM 콘텐츠에 대한 M3U8 응답 데이터를 반환하지 않음 PTMediaPlayerItem.prepareToPlay에 있는 매니페스트 파일의 초기 로드에서 로드가 실패하면 TVSDK가 실패 응답의 본문을 애플리케이션에 보고하지 않습니다.
이 문제는 TVSDK가 실패 응답을 애플리케이션에 오류로 보고하도록 허용함으로써 해결되었습니다.

* Zendesk #19701 - SAP/불연속으로 재생 중단 오디오 및 비디오가 불연속으로 정렬되지 않으면 플레이어가 중지됩니다.

* 버그 #PTPLAY-11162 - 버전 1.0.2f에 대한 OpenSSL 라이브러리 업데이트가 해결되었습니다.

**버전 1.4.20(1546)**

* Zendesk #17384 - 기능 요청: AAC 미디어의 ID3 태그에 대한 AAC 재생 지원 ID3 메타데이터 는 버전 1.4.20부터 Android용 TVSDK에서 제공됩니다.

* Zendesk #18358 - 플레이어가 동기화 중단 없이 비트율 스위치를 중지합니다. 이 문제는 ABR 스티칭 에지 케이스를 적절하게 처리하여 해결되었습니다.

* Zendesk #19232 - TVSDK 1.4.18을 사용하는 앱은 이전 Amazon OS 버전 4에서 이상하게 동작합니다. 이 문제는 Android Webview를 지원하지 않는 장치와의 충돌을 방지하기 위해 TVSDK 플레이어 초기화 프로세스에서 숨겨진 웹 보기 생성을 제거하여 해결되었습니다.

* Zendesk #19585 - 적응형 비트율 전환이 발생할 때 슬로우 모션 재생.
ABR 전환 중에 새 프로필의 오디오 샘플링 속도가 현재 프로필과 다른 경우 재생이 빨라지거나 느려집니다. 이는 비디오 발표자에게 오디오 형식이 변경되었다는 알림이 전송되지 않기 때문입니다.
이 문제는 알림 플래그가 올바른 위치에 설정되어 있는지 확인하여 해결되었습니다.

* Zendesk #19683 - SAP DAI 재생 - 몇 초 동안 오디오가 없습니다.
TVSDK의 논리에 있는 여러 사례의 경우, 두 렌디션 세그먼트의 타임스탬프를 비교하면 타임스탬프가 항상 0ms 차이로 일치할 수 없기 때문에 RENDITION_TIMEOUT_THRESHOLD이 값의 허용 범위로 사용되었습니다. 간격이 RENDITION_TIMEOUT_THRESHOLD 범위 내에 있으면 일치한다고 가정합니다.

RENDITION_TIMEOUT_THRESHOLD이 100ms로 설정되었지만 특정 스트림에 대해 불충분한 것으로 나타났습니다. 이 문제는 RENDITION_TIMEOUT_THRESHOLD을 200ms로 늘려서 해결되었습니다.

* Zendesk #19699 - TVSDK가 VTT 자막 트랙 간에 전환할 수 없음 트랙이 변경될 때 플레이어를 덤프하고 매니페스트를 다시 로드하여 이 문제를 해결했습니다. 또한 2바이트 WebVTT 자막 트랙 이름에 영향을 주는 UTF8 문자열 변환 문제를 수정했습니다.

* Zendesk #19717 - CC 옵션에 문제가 표시됨 이 문제는 유니코드 문자열을 올바르게 처리하여 해결되었습니다.

* Zendesk #19910 - TIT2 ID3 태그가 검색되지 않음 ID3 v2.4 문자열 인코딩과 ID3 v2.3에 대한 지원을 보다 완벽하게 제공하여 이 문제를 해결했습니다.

* Zendesk #20135 - TVSDK가 VOD 콘텐츠에 대한 여러 onComplete를 트리거하고 있습니다.
이 문제는 상태 변경 이벤트의 전체 경우가 아니라 적절한 위치에 post_roll_complete 이벤트 리스너를 추가하여 해결되었습니다.

**버전 1.4.19(1521)**

* Zendesk #4180 - TVSDK가 HDCP를 적용하지 않습니다.
   * 이는 이 티켓의 부분 수정 사항이며 NVidia 실드 장치의 문제만 해결합니다.
HDCP 상태를 동적으로 추적하려면 Nvidia Shield에서 올바르게 구현된 HDCP 탐지 API를 사용해야 합니다.

* Zendesk #18358 - TVSDK가 동기화 중단 없이 비트율 스위치를 중지합니다.
   * 이 문제는 PTS 불연속성을 감지하기 위한 새로운 경고를 추가하고 모든 ABR 스위치에 대한 올바른 세그먼트 검색을 다시 수행하도록 PTS 검사를 강제함으로써 해결되었습니다.
고정 문제를 해결하려면 mediaPlayer.setCustomConfiguration 메서드 호출에 forcePTSCheckForABR을 인수로 포함해야 합니다.

* Zendesk #19038 - Asus Zenpad 10에 라이브 스트림 없음.

  이 문제는 미디어 코덱 정보를 미리 로드하여 해결되었으므로 런타임에 함수를 쿼리하지 않습니다.

* 다음 문제는 Zendesk 보고서와 #19038.
   * Zendesk #19483 - TVSDK가 인텔 플랫폼에서 충돌합니다.
   * Zendesk #19171 - Android 5.0의 Asus Memo Pad 7에서 충돌합니다.

**버전 1.4.18 (1503)**

* Zendesk #3324 - Primetime 광고 보고는 VMAP에 광고 미디어가 없을 때 광고 브레이크를 추적하지 않습니다.
광고 브레이크가 비어 있는 경우 광고 브레이크 시작 및 전체 추적 이벤트가 핑되지 않았습니다. 이 문제는 유효한 AdSource 노드가 있는 VMAP AdBreak와 같은 빈 광고 브레이크에서 광고 브레이크 시작 Ping을 전송하여 해결되었습니다.

* Zendesk #18229 - MediaPlayer.reset() 호출 후 SetCCVisibility(VISIBLE)가 무시됩니다. 이 문제는 MediaPlayer 클래스의 reset() 함수에 setCCVisibility(Visibility.INVISIBLE);을 추가하여 해결되었습니다.

* Zendesk #18328 - 60FPS가 있는 콘텐츠의 Amazon Fire TV 2세대 장치에서 프레임 드롭 문제 이 문제는 수면 시간 의사 결정에 대해 인코딩된 FPS를 적용하고 더 나은 인코딩된 FPS 예측 논리를 사용하여 해결되었습니다.

**버전 1.4.17(1472)**

* Zendesk #2231 - MediaPlayerNotification에서 사용할 수 없는 매니페스트를 가져오는 중 오류가 반환됨 구문 분석 오류가 있을 때 매니페스트의 응답 본문을 포함하여 이 문제를 해결했습니다.

* Zendesk #17703 - VideoEngineView는 비디오 재생 중 스크린샷을 방지하지 않습니다. setSecure 메서드는 API 17 이후 사용할 수 있지만 API 17이 4.2, 4.2.1 및 4.2.2를 포함하므로 어떤 예외가 발생하는지 또는 장치별로 발생하는지 알 수 없습니다. 이 문제는 VideoEngineView.setSecure를 try catch 절에 래핑하여 해결되었습니다.

* Zendesk #17919 - 컨텐츠 찾기로 인해 하트비트 오류 발생 프리롤 후 찾기가 시작될 때 생성된 하트비트 호출의 결과로 잘못된 입력 데이터 위치 오류가 발생했습니다. 이 문제는 해결되었습니다.

**1.4.16a** (1454a)

* Zendesk #18215 - 일부 AES 스트림을 로드할 수 없습니다.
이 문제는 AES 키를 로드하기 전에 프로필 DRM 메타데이터 크기를 확인하여 해결되었습니다.

**버전 1.4.16 (1454)**

* Zendesk #3875 - TVSDK가 이제 curl 대신 httpurlconnection을 직접 사용하므로 재생 중에 탭 S가 충돌하고 CRS에 대한 Auditude 시 OKHTTP 종속성을 되돌립니다. 다른 JNI 호출을 수행하기 전에 예외를 지움으로써 문제가 해결되었습니다.

* Zendesk #4487 - 콘텐츠의 선형 채널 추적 선형 스트림 재생 세션 중에 비디오 하트비트 추적기를 다시 초기화할 수 있으므로 문제가 해결되었습니다.

* Zendesk #17919 - Android - 콘텐츠 찾기로 인해 하트비트 오류 발생 챕터에 찾기가 있을 때 하트비트가 오류 상태에 있을 때 문제가 해결되었습니다.

* Zendesk #18053 - Adobe Primetime이 Marshmallow에서 충돌함 TVSDK 라이브러리가 YUV -> RGB 색상 변환을 수행하는 네온 코드를 사용할 때 Android M OS에서 TVSDK가 충돌했습니다. 이 문제의 원인이 되는 함수를 비-네온 버전의 코드를 사용하여 업데이트하여 문제를 해결했습니다.

* Zendesk #18072 - Android M - 애플리케이션 충돌 프로필 및 수준이 지원되는지 확인할 때 MediaCodecList 및 MediaCodecInfo API를 호출할 때 충돌이 발생합니다. 코덱 정보가 필요한 경우에만 이러한 API를 호출하지 않도록 모든 코덱 정보를 미리 로드하여 임시 작업을 제공함으로써 문제를 해결했습니다.

* Zendesk #18074 - Android 6.0에서 Nexus에서 아랍어 자막이 작동하지 않습니다. 이 문제는 Android에 대한 CTS 글꼴 맵 지원을 제공하여 해결되었습니다.

**버전 1.4.15 업데이트(1438)**

* Zendesk #17437 - 일부 AES 스트림으로 VOD 콘텐츠 시작이 오래 지연됩니다.
이 문제를 해결하려면 매니페스트에 여러 키가 나열되어 있는 경우 모든 AES 키를 동시에 다운로드하십시오.

**버전 1.4.15(1435)**

* Zendesk #4278 - 적응형 비트율 변경(ABR) 시 Android 셋톱 박스의 결함.
수정 사항은 최신 Android 미디어 코덱이 있는 원활한 ABR 스위치에 대한 지원을 추가하는 것이었습니다.

* Zendesk #17063 - mediaPlayer.reset()을 호출하면 비디오 엔진 재설정 오류가 발생합니다.
ErrorEvents를 발송할 때 VideoEngineExceptions의 원래 MediaErrorCode를 포함하도록 수정되었습니다.

* Zendesk #17130 - FireTV에서 볼 수있는 비트 전송률을 변경할 때 짧지만 눈에 띄는 일시 정지.
(위의 #4278과 동일) 최신 Android 미디어 코덱이 있는 매끄러운 ABR 스위치에 대한 지원을 추가하는 것이 해결되었습니다.

* Zendesk #17666 - 콘텐츠를 다시 시작할 때 예기치 않거나 광고가 없는 추가 광고 마커.
prepareToPlay on video-on-demand(VOD) 컨텐츠를 수행할 때 가상 시간이 아닌 로컬 시간에 초기 찾기가 수행되는 문제가 수정되었습니다.

* Zendesk #17437 - 일부 AES 스트림으로 VOD 콘텐츠 시작이 오래 지연됩니다.
매니페스트에 여러 키가 나열되어 있을 때 모든 AES 키를 동시에 다운로드하는 것이 해결되었습니다.

* Zendesk #17851 - Android TV - ABR 동안의 블랙 프레임 수정 사항은 KEY_MAX_WIDTH 및 KEY_MAX_HEIGHT를 지정하여 적응형 재생을 활성화했습니다.

**버전 1.4.14(1415)**

* Zendesk #3875 - 재생 중 탭 S가 충돌합니다.
추락을 방지하기 위해 추가 수리가 필요했다.

* Zendesk #17245 - Android TV의 폴백이 작동하지 않습니다.
폴백이 활성화된 경우 재생이 중단되고 VMAP 응답에 빈 광고 브레이크가 있는 추가 문제를 해결했습니다.

**버전 1.4.14(1412)**

* Zendesk #17245 - Android TV의 폴백이 작동하지 않습니다.
대체 광고에서 크리에이티브 리패키징을 비활성화하기 위한 제한을 제거했습니다.

**버전 1.4.13(1388)**

* Zendesk #3502 - 광고 브레이크 기간 동안 HLS 클라이언트 기반 장애 조치(Failover) 지원 라이브 프로필 업데이트 시 기본 매니페스트로 장애 조치 허용(Allow failover) 오류가 광고 브레이크 기간 동안 발생합니다.

* Zendesk #3875 - 재생 중에 탭 S가 충돌합니다. HttpUrlConnection과 cURLm 간의 충돌을 해결하려면 타사 라이브러리를 사용합니다.

* Zendesk #4450 - 콘텐츠 해결자의 단일 배치에 대한 사용자 지정 메타데이터 설정 문제 Opportunity 설정에 setter 를 추가합니다.

**버전 1.4.12(1388)**

* Zendesk #2751 - CSAI 및 CRS | 개선: 특정 미디어 파일 URL에서 동적 요소를 처리합니다.
동적 크리에이티브 URL이 포함된 광고를 제대로 처리하도록 Creative Repackaging Service 가 업데이트되었습니다.

* Zendesk #3965 - trickplay에서 일반 재생으로 전환하면 재생을 시작하기 전에 조금 앞으로 이동합니다.
   * 수정 사항에는 GetStreamTime을 계산하는 대신 모든 변수가 업데이트될 때까지 속도가 변경되기 전 시간을 반환하는 TVSDK가 포함되어 있습니다.
   * 스트림 끝 근처에서 트릭 플레이 속도를 변경할 때 충돌을 해결했습니다.
   * 트릭 재생 중에 현재 시간 계산을 수정했습니다.

* Zendesk #3978 - 8x 및 16x에서 트리크플레이가 자주 멈춥니다.
   * 항상 지속적인 버퍼링을 방지하기 위해 비트 전송률이 가장 낮은 트릭 플레이 프로필을 선택하십시오.
   * 높은 트릭 재생 속도를 위해 건너뛰기 프레임 간격을 늘립니다.
   * 트릭 플레이 중에 버퍼가 목표 길이에 도달한 후 계속 증가하는 문제를 해결합니다.

* Zendesk #3992 - 추가 Trickplay 속도.
TrickPlay는 16x보다 높은 비율을 수락하도록 업데이트되었습니다. 이제 +/- 32, +/-64 및 +/-128도 허용됩니다.

* Zendesk #4007 - GEOB 개체를 타임라인 메타데이터의 일부로 해석합니다(Android 및 웹).
setByteArray 및 getByteArray API를 추가했습니다.

* PTPLAY-7301 - 임의 액세스 포인트에서 즉시 시작.
0이 아닌 시작점을 허용하도록 인스턴트 온이 업데이트되었습니다.

**버전 1.4.11(1363)**

* Zendesk #2076 - Android 4.0.3으로 Motorola Xoom에서 비디오를 재생할 때 자주 더듬거림 그들이 높은 프로필을 재생하려고하지 않도록 장치를 허용 목록에 추가.

* 젠데스크 #2197 - `[Ads]` 광고 오류 추적 - 경고 알림과 함께 OperationFailedEvent를 발송합니다.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 매크로가 채워지지 않음
   * 인라인 광고에 잘못된 크리에이티브가 있는 경우 오류 코드 400이 표시됩니다.
   * `[ERRORCODE]` 매크로는 URL로 인코딩됩니다.

**버전 1.4.10(1354)**

* Zendesk #2941 - 라이브 에셋에 검색 가능한 범위에서 &quot;0&quot;이(가) 없습니다. 이전에는 라이브 스트림의 시작을 찾을 때 3 세그먼트 버퍼가 있었으며, 이제 라이브 스트림의 바로 시작(즉, 첫 번째 세그먼트의 시작)을 찾을 수 있습니다.

* Zendesk #3169 - Adobe Analytics 통합으로 참조 플레이어 업데이트참조 플레이어가 예제 삽입으로 Adobe Analytics 라이브러리로 업데이트되었습니다.
* Zendesk #3299 - 설명할 수 없는 트릭 플레이 동작
   * 트릭 재생을 중지한 후 재생 상태로 돌아가는 데 몇 초(경우에 따라 25초 이상)가 걸릴 수 있는 버그를 수정했습니다.
   * 동일한 미디어에서 trick play를 두 번 호출하면 현재 시간에 스트림이 중지될 수 있는 버그를 수정했습니다.
* Zendesk #3433 - Android 및 Flash - 자막 문제

WebVTT용 GetLine이 &lt;cr>&lt;lf> 패킷의 길이가 조정되었습니다. 마지막 캡션에는 이전 캡션의 문자가 포함될 수 있습니다.

* PTPLAY-6243 - 참조 플레이어를 개선하여 디버그 정보 캡처

Android 샘플 참조 플레이어가 디버그 로그를 켜고 결과를 이메일로 보내는 옵션으로 향상되었습니다. 이 옵션은 참조 플레이어의 로그 메뉴에 있습니다.

**버전 1.4.9(1332)**

* Zendesk #2649 - 버퍼 완료는 초기 버퍼가 가득 차기 전에 발생합니다.

찾기 후 비디오 발표자가 재생할 준비가 되기 전에 비디오 엔진이 상태를 재생 중 으로 설정하는 경우일 수 있습니다. 찾기 전에 버퍼 상태가 높으면 발생합니다. 비디오 엔진에 낮은 버퍼 상태를 알려 수정합니다. 비디오 엔진 버퍼 상태가 낮은 경우 재생 을 호출하면 재생 이 아닌 버퍼링 으로 상태가 변경됩니다. 상태가 [재생]으로 변경되면 재생이 다시 시작됩니다.

* Zendesk #2846 - 개선 요청: Auditude 라이브러리에서 수행한 호출에 대해 서로 다른 사용자 에이전트 문자열을 설정하는 기능을 제공합니다.

광고 관련 호출에 대한 사용자 에이전트 auditudeSettings.setUserAgent(&quot;user/agent&quot;)를 설정하기 위해 새 API가 추가되었습니다. 설정된 사용자 에이전트가 없으면 기본값이 사용됩니다. 이 기능은 광고 관련 호출의 사용자 에이전트에만 영향을 주며, 미디어 호출의 사용자 에이전트는 &quot;Adobe Primetime&quot;+로 변경되지 않습니다.&lt;default useragent=&quot;&quot;>.

**버전 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 로컬 오류... FragmentedHTTPStreamer::ThreadParseManifest()에서 매니페스트를 로드할 수 없는 경우 URL 도메인이 localhost인지 확인하고, localhost이면 도메인을 127.0.0.1로 변경하고 ThreadParseManifest를 회수합니다.
* Zendesk #3072 - 낮은 비트율로 자동 전환합니다. 0 PTS 페이로드를 건너뛰도록 버퍼 길이 계산을 변경했습니다.
* Zendesk #3168 - WebVTT 자막은 처음 10초 동안만 표시됩니다.
* Zendesk #3193 - TVSDK, PlaybackEventListener.onProfileChanged()의 프로필 변경 API 요청이 추가되었습니다.

**버전 1.4.7 (1311)**

* Zendesk #2197 - 광고 오류 추적. 매니페스트를 로드하지 못한 자산에 대한 알림을 추가했습니다.
* Zendesk #2575 - PSDK가 비디오 전에 MARK 사용자 지정 스트림 내 광고를 무시합니다.
* Zendesk #2719 - Auditude 광고가 있는 Win Death, auditude 플러그인의 상대 URL로 리디렉션될 때 비콘 추적을 고정
* Zendesk #2760 - TrickPlay 모드 중에 DISCONTINUITY 태그가 무시됨
* Zendesk #2805 - 재생 시작 시 플레이어 충돌, Zendesk #2719과 동일한 수정
* Zendesk #2817 - Android 플레이어 - 디코드 버퍼를 2.0초에서 3.0초로 확장하여 플레이어가 때때로 정지되고 재생이 중지됩니다.
* Zendesk #2839 - Adobe Primetime PSDK가 ARMv8 칩셋을 지원합니까?, Galaxy S6에서 발견된 충돌 수정 사항을 추가했습니다.
* Zendesk #2885 - Auditude 충돌 재생, Zendesk #2719과 동일한 수정
* Zendesk #2895 - 재생 10분 후에도 지속적으로 라이브 HLS 실패
* Zendesk #2925 - 입력 큐에 패킷을 대기시킬 때 특정 장치에서 Android 개발 빌드(1.4.5)에 대한 피드백, PTS가 음수이면 디코더는 이상한 상태로 전환되어 향후 패킷에 대해 항상 음성 출력 PTS를 받습니다. 이 문제를 방지하기 위해 음수일 경우 수정 사항은 입력 PTS를 0으로 설정합니다.
* PTPLAY-4645 - openssl에서 RC4 암호 지원을 끕니다. RC4에 대한 알려진 업적들이 있다. 이는 RC4만 지원하는 서버와 접속하려고 하면 실패함을 의미한다.

**버전 1.4.6 (1282)**

* Zendesk #2192 - 고속 스위치 구현을 제거하여 수정되는 열악한 네트워크 조건에서 비트율이 항상 낮아지는 것은 아닙니다.
* Zendesk #2631 - Android의 아랍어 자막: 아랍어 글꼴의 글꼴 크기를 조정하여 여러 줄의 텍스트가 잘린 상태로 표시됩니다.
* Zendesk #2844 - 참고 4 및 조각 다운로드 시간의 버퍼링은 정확하지 않습니다.

이 문제는 비디오 세그먼트 다운로드 간 지연 시간을 대역폭 계산에 추가하고 다운로드 시간 계산 로직에서 전체 요청 주기 시간을 사용하도록 하여 해결되었습니다.

* Zendesk #2908 - 다음 5, 6 및 7에서 아랍어 자막이 작동하지 않습니다, 아랍어 스크립트에 대 한 2 대체 글꼴을 추가하여 수정.
* PTPLAY-4627 - Nielson appsdk를 버전 1.2.3.7로 업데이트
* PTPLAY-5084 - 라이브 기본 매니페스트 업데이트 장애 조치(failover) 지원

**버전 1.4.5(1248)**

* Zendesk #1757 - 일부 비디오 비트 전송률 프로필에 대해 오디오만 재생되거나 플레이어가 충돌하는 경우, Nexus 4 및 Nexus 7 충돌이 수정되었습니다.
* Zendesk #2072 - AdEvent용 TimedMetadata에 전체 URL &quot;http&quot;만 포함되어 있지 않음
* Zendesk #2192 - 낮은 네트워크 조건에서 비트율이 항상 낮아지는 것은 아닙니다.
* Zendesk #2256 - 기본 재생 목록에 액세스하고, 마스터 재생 목록의 구독한 태그에 대해 timedMetadata 이벤트를 발송하도록 PSDK를 업데이트했습니다.
* Zendesk #2269 - WebVTT를 사용하여 두 개의 다른 자막 언어가 동시에 화면에 나타납니다.
* Zendesk #2417 - 플레이어가 재생을 시작하기 전에 자막을 다운로드하려고 하는 동안 WebVTT가 세그먼트 번호 일치를 위해 잘못된 세그먼트 번호 변수를 사용했습니다. 버그는 0부터 시작하는 세그먼트 인덱스가 있는 미디어에 대해서만 표시됩니다.
* Zendesk #2470 - 일시 중단 후 비트율 변경이 발생할 때 PSDK가 일시 중단 상태에서 반환되지 않습니다. RestoreGPUResource(일시 중단 상태에서 플레이어 복원)에 의해 스마트 찾기가 호출되고 그 전에 스트림 스위치가 검색되는 특수한 상황에서 스마트 찾기를 완료할 수 없어 지속적인 버퍼링이 발생합니다.
* Zendesk #2451 - 자막 &#39;bottom inset&#39;, 캡션 코드에 &#39;bottomInset&#39; 매개 변수 추가
* Zendesk #2480 - HTTP 302 리디렉션 최적화 비활성화, useRedirectedUrl 속성 설정에 대한 지원 추가
* Zendesk #2486 - 타사 비콘
* Zendesk #2547 - 아랍어 자막: 텍스트를 오른쪽으로 정렬해야 함

**버전 1.4.4 (1195)**

* Zendesk #1158 - Huawei Valiant(Y301A1)에서 재생이 실패합니다.
* Zendesk #1709 - 잘못된 미디어 크기 및 스트레치된 비디오
* Zendesk #1757 - 동일한 spa/pps 데이터가 있는 스트림 간에 프로필 전환 후 재생되는 오디오만 해당
* Zendesk #2095 - HTTP 307 상태(리디렉션)로 인해 Adobe 플레이어가 재생을 중지함
* Zendesk #2126 - 마지막 ADEVENT에 대한 TimedMetaData 이벤트 누락, 마지막 세그먼트 다음에 존재하는 구독한 태그는 AVE에서 PSDK로 보고되지 않았습니다.
* Zendesk #2227 - VideoEngine nativeReset 및 nativePause의 잠금
* 버그 #3921755 - OpenSSL 라이브러리가 버전 1.0.1L로 업데이트됨

**버전 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - 자막 켜기 및 끄기
* PTPLAY-1818 - 리와인드 트릭 플레이는 그것을 뒤로 되감는 대신 광고에서 멈춥니다
* PTPLAY-2736 - WebVTT 캡션이 있는 스트림이 재생을 완료하면 이전에 표시된 WebVTT 캡션이 화면에 표시됩니다.
* PTPLAY-3773 - 광고 위치 후 스트림 재생이 시작되면 미드롤 광고가 재생되지 않습니다

**버전 1.4.2**

* Zendesk #1561 - primetime의 HLS 클라이언트 기반 페일오버 지원 프로그램 날짜 시간을 사용하여 장애 조치(failover) 해결
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0입니다(오디오 전용으로 고정되지 않음).
* Zendesk #1626 - 플레이어에서 잠재적인 메모리 누수. 실제 메모리 누수가 아닙니다. NotificationHistory에서 최근 1000개의 알림을 저장하는 문제가 발생했습니다. 100개로 줄었습니다.
* Zendesk #2192 - 낮은 네트워크 조건에서 비트율이 항상 낮아지는 것은 아닙니다.

**버전 1.4.1(1121)**

* Zendesk #1951 - 4.0.x 장치에서 VideoEngine.nativeReset() 의 작동 중지
* Zendesk #2064 - 특정 인텔 기반 Android 장치를 기반으로 한 기본 충돌 SIGSEGV
* Zendesk #2075 - 4.0.x 장치에서 VideoEngine.nativeReleaseGPUResource의 작동 중지 &#42;&#42;&#42;필수&#42;&#42;&#42; android 5.0(Lollipop) 지원
* Zendesk #1513 - Android Lollipop 지원
* Zendesk #1709 - 잘못된 미디어 크기 및 스트레치된 비디오
* Zendesk #1871 - WebVTT 캡션이 있는 라이브 스트림을 볼 때 WebVTT 캡션이 간혹 사라졌다가 다시 나타납니다
* Zendesk #1996 - PSDK 1.4.0에 타임라인 마커가 표시되지 않음
* Zendesk #2046 - PSDK 1.4.1.1113과 충돌, 감도에서 광고가 반환되지 않을 때 라이브 스트림에 대한 충돌을 해결했습니다.
* 버그 #3769657 - curl 버전을 7.38.0으로 업데이트
* PTPLAY-1575 - ABR 재생이 오디오 전용 스트림으로 시작된 다음 오디오/비디오 스트림으로 전환되면 오디오가 계속되는 동안 비디오가 렌더링되지 않습니다
* PTPLAY-2499 - 최근 취약점을 해결하기 위해 OpenSSL을 버전 1.0.1j로 업데이트
* PTPLAY-2632 - Android Lollipop에서 미드롤 광고 완료 후 비디오가 복구되지 않음
* PTPLAY-2678 - Android Lollipop의 라이브 장수 테스트 중 비디오 중단

**버전 1.4.0**

* Zendesk #1024 - 매니페스트를 통해 스트림에서 광고를 제거하는 기능
* Zendesk #1293 - 자막 트랙 선택 문제.
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0이며 mediaDuration은 이제 올바른 값을 표시합니다.
* Zendesk #1629 - Galaxy S4에서 광고 재생 종료 시 플레이어/앱 충돌
* Zendesk #1674 - ClosedCaption이 표시되지 않습니다. 0x03 ETX 코드가 없을 경우 708 캡션이 표시됩니다.
* PTPLAY-2157 - 스트림에서 다른 스타일이 설정되고 시각적으로 확인된 후에도 getters에 의해 기본 폐쇄 캡션 스타일이 반환되었습니다. 이제 폐쇄 캡션 스타일 속성에 설정된 값이 표시됩니다.

## 1.4의 알려진 문제 {#known-issues-in}

**버전 1.4.31**

* PTPLAY-16803 - 캡션 시스템이 작동하려면 비디오가 필요하므로 닫힌 캡션은 오디오 전용 콘텐츠에서는 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없고 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* PTPLAY-1634 - 동일한 구독 태그에 다른 라이브 창에서 다른 타임스탬프가 있습니다. 라이브 창이 이동할 때 해당 창의 동일한 태그에 동일한 타임스탬프가 있어야 합니다. 그러나 동일한 태그에도 서로 다른 타임스탬프가 있는 경우가 있습니다.
* PTPLAY-3197 - ~ 1시간의 연속 재생 후 Acer Iconia 장치에서 신호 11 SIGSEGV 오류와 충돌
* PTPLAY-3310 - 일부 낮은 비트율 오디오를 사용하면 Acer Iconia에서 오디오가 고르지/말을 잃게 됩니다
* PTPLAY-3355 - WIN DEATH 충돌 모토로라 줌, 4.0.x ~ 1시간 동안 연속 재생 후.
* PTPLAY-3557 - 광고 브레이크에서 되감는 중 스트림이 완료됨
* PTPLAY-7079 - Android 클라이언트의 재생 창이 보안 중지/하드 중지와 작동하지 않음
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 이동하거나 펄스로 나타날 수 있습니다. 정밀한 조사하에서만 관측할 수 있다
* 버그 #3761170 - Ads로 라이브의 seekToLocal은 라이브 스트림에 currentTime API를 사용하는 최선의 방법인 광고 콘텐츠로 다시 이동할 수 없습니다.
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 하는 경우 종종 두 개의 광고 마커가 함께 가깝게 표시됩니다. 이러한 광고 마커는 동일한 광고를 나타내며 하나만 재생됩니다
* 버그 #3763373 - VOD 스트림에 광고를 지나서 탐색할 때 광고 마커가 잠시 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 악영향이 없습니다
* 일부 장치에는 알려진 재생 문제가 있습니다. 다음을 참조하십시오 [1.4의 알려진 장치 문제](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 참조 구현 - 샘플 애플리케이션에서는 트릭 플레이가 구현되지 않습니다.
* 일부 Android TV 장치에서는 다음 전환 지점에서 디코더 재설정으로 인해 검은색 프레임이 표시됩니다.
   * 트리크플레이 모드 안과 밖
   * 지연 바인딩 오디오 트랙 간 전환
   * 광고에서 기본 컨텐츠로.

**버전 1.4.23**

* 캡션 시스템이 작동하려면 비디오가 필요하기 때문에 닫힌 캡션은 오디오 전용 콘텐츠에서는 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없고 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* 버전 1.4.23부터 TVSDK는 Gingerbread OS 2.3을 지원하지 않습니다. 이는 TVSDK가 다음의 사설 Android 라이브러리를 사용하여 Gingerbread OS가 있는 장치에 대한 하드웨어 정보를 수집했기 때문입니다.

   * `libstagefright.so`
   * `libcutils.so`

Android N 릴리스에서 Google은 이러한 개인 라이브러리에 대한 액세스를 제거했습니다. 진저브레드 OS는 현재 전 세계 안드로이드 OS 시장 점유율 1% 미만을 차지하고 있어 버전 1.4.23 이후에는 더 이상 진저브레드 OS가 TVSDK에서 지원되지 않게 된다.
버전 1.4.23(Android N 지원 포함) 이상을 사용하는 경우:
* minSdkVersion 11을 사용하도록 앱을 업데이트합니다.
* 최종 사용자가 OS 2.3을 실행 중인 경우 SDK 버전은 애플리케이션의 minSdkVersion 보다 낮습니다. 응용 프로그램의 설치 또는 업그레이드가 중단됩니다.
* 최종 사용자가 OS 2.3보다 높은 버전을 실행 중인 경우 애플리케이션이 올바르게 설치됩니다.

minSdkVersion 을 업데이트하는 경우:

* 최종 사용자가 OS 2.3을 실행 중인 경우 애플리케이션이 설치되지만 재생이 작동하지 않습니다.
이 설정은 업데이트 및 새로 설치 모두에 적용됩니다.
* 최종 사용자가 OS 2.3 이상의 시스템을 실행 중인 경우 앱이 올바르게 설치되고 콘텐츠가 올바르게 재생됩니다.

**버전 1.4.22**

* 스플라이스 아웃과 스플라이스 인 태그가 서로 너무 가까우면 광고의 조기 종료가 일부 중간 롤 광고에서 작동하지 않습니다.

**버전 1.4.2**

* 광고 브레이크 시 되감기로 인해 스트림이 완료됩니다.

광고 경계에 도달하면 트릭 재생 되감기 작업 중에 미디어 플레이어가 MediaPlayerState.Complete를 잘못 보냅니다. 트릭 재생 모드에 있는 경우 플레이어는 이 이벤트를 무시해야 합니다. 그렇지 않으면 SDK가 상태를 올바르게 처리합니다.

**버전 1.4.0(1086)**

* PTPLAY-1634 - 동일한 가입 태그에 다른 라이브 창에서 다른 타임스탬프가 있습니다. 라이브 창이 이동할 때 각 창의 동일한 태그에 동일한 타임스탬프가 있어야 합니다. 그러나 동일한 태그에도 서로 다른 타임스탬프가 있는 경우가 있습니다.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE는 일시 중단에서 대체 스트림으로/로부터 여러 번 전환된 후에 표시되는 경우가 있습니다.
* 버그 #3726865 - MultiBitrate LBA 스트림이 오디오 전용 스트림에서 시작하는 경우 오디오/비디오 스트림으로 전환되면 비디오가 표시되지 않습니다. 오디오/비디오 스트림에서 시작하면 이 문제가 표시되지 않으며 오디오 및 오디오/비디오 스트림 간을 성공적으로 전환할 수 있습니다
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 이동하거나 펄스로 나타날 수 있습니다. 정밀한 조사하에서만 관측할 수 있다
* 버그 #3761170 - Ads로 라이브의 seekToLocal은 광고 콘텐츠로 다시 이동할 수 없습니다. 라이브 스트림에 currentTime API를 사용하는 것이 가장 좋습니다
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 하는 경우 종종 두 개의 광고 마커가 함께 가깝게 표시됩니다. 이러한 광고 마커는 동일한 광고를 나타내며 하나만 재생됩니다
* 버그 #3763373 - VOD 스트림에 광고를 지나서 탐색할 때 광고 마커가 잠시 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 악영향이 없습니다
* 일부 장치에는 알려진 재생 문제가 있습니다. 자세한 내용은 [1.4의 알려진 장치 문제](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 참조 구현 - 샘플 애플리케이션에서는 트릭 플레이가 구현되지 않습니다.

## 1.4의 알려진 장치 문제 {#known-device-issues-in}

| 장치 | 칩셋 | 문제 | 원인 | 해결 방법 |
|--- |--- |--- |--- |--- |
| 드로이드 | TI 오맵3 | 디코더를 다시 시작하는 중이므로 ABR 지연이 예상됩니다. |  |  |
| HTC 욕구 (다른 HTC 욕구 HD) | QSD8250 | 비디오를 재생할 수 없습니다. VIDEO_PROFILE_NOT_SUPPORTED 오류를 반환합니다. | 욕구는 적절한 HW 디코더를 제공하지 않는다. Stagefright의 SW 디코더를 제공합니다. | 장치를 다시 시작합니다. |
| HTC EVO 4G | QSD8650 | HW 디코더가 없습니다. | Qualcomm에는 HW 디코더가 없습니다. | Android 4.x로 업그레이드하십시오. |
| Kindle FireSystem 버전 6.0 | TI 오맵4 | HLS 스트림을 재생하지 않습니다. AIR에 대한 비디오가 작동하지 않습니다. |  | 시스템 버전 6.3으로 업그레이드하십시오. |
| 킨들 파이어 HD | TI 오맵4 | 비디오를 재생할 수 없는 상태가 될 수 있습니다. VIDEO_PROFILE_NOT_SUPPORTED 및 UNRECOVERABLE_ERROR 오류를 반환합니다. | HW 디코더는 앱이 HW 디코더를 완전히 종료하지 않을 때, 예를 들어, 충돌이 발생한 후에 복구할 수 없는 상태가 된다. 디바이스의 기본 앱에서도 발생합니다. | 장치를 다시 시작합니다. |
| 킨들 파이어 HD 8.9 | 스냅드래곤 | 여러 ABR 스위치 후 AVE가 충돌합니다. |  |  |
| 모토로라 아트릭스 | Tegra2 | AIR이 아닌 AVE의 전반적인 성능 문제입니다. 오디오/비디오가 동기화되지 않아 9분에서 15분 사이에 재생되면 비디오 재생이 중지됩니다. 충돌합니다. | AIR에서 활성화하는 openGLES와 관련이 있을 수 있습니다. 조사 중입니다. |  |
| Nexus 7(2세대) | S4Pro APQ8064(Qualcomm) | 동영상이 30분 이상 일시 중지되면 장치가 중단됩니다. | Google에 보고된 디바이스 문제입니다. | 긴 일시 중지 상태를 허용하지 않도록 앱을 시간 초과해야 합니다. |
| Nexus S(GB) | 허밍 버드 | HW 디코더를 사용하여 비디오를 재생할 수 없습니다. | Nexus S에는 Stagefright 기반 HW 디코더가 없으므로 Android 2.3의 경우 SW 디코더를 사용합니다. | ICS로 업그레이드하십시오. |
| Nexus S (ICS) | 허밍 버드 | 비디오가 깜박이는 경우가 가끔 있습니다. | 잘못된 데이터는 디코더가 잘못된 상태에 빠지게 할 수 있습니다. | 장치를 다시 시작합니다. |
| Nook tabletAndroid OS: 2.3 | TI 오맵 | 비디오가 재생되지 않고 앱이 중단됩니다. | Stagefright는 앱을 몇 번 실행한 후 불안정한 상태로 들어갑니다. mediaplayer::QueryCodecs에 대한 호출이 중단됩니다. | 장치를 다시 시작하여 상태를 재설정합니다. |
| 삼성 갤럭시 에이스 | Qualcomm MSM7227 | SampleMediaPlayer 앱을 설치할 수 없습니다. | 보다 일반적인 ARM v7 칩셋 대신 ARM v6를 사용합니다. FP/AIR은 이 장치를 지원하지 않습니다. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | 노바토르 | 비디오를 재생할 수 없습니다. | 이 칩셋은 AVE의 Android 사전 ICS용 알 수 없는 디코더입니다. |  |
| Samsung Galaxy S2 (GT-I9100) | 엑시노스 | 이 장치의 비디오 성능이 최대가 아닙니다. | HW 디코더는 잘못된 PTS를 갖는 디코딩된 프레임들을 반환하고 있다. 디코더가 프레젠테이션 시간 대신 디코딩 시간을 사용하는 것 같습니다. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI 오맵4 | 비디오를 시작할 때 충돌합니다. |  | Android 2.3.7 또는 4.x로 업그레이드하십시오. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | 간헐적으로 비디오가 정지하고 오디오만 재생된 후 응답하지 않습니다. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | 비디오가 중지됩니다. | 조사 중입니다. |  |
| Samsung 갤럭시 탭 1 v10.1 | 테그라 | MBR 전환은 최대 3초 정도 소요될 수 있습니다. | MBR 충돌을 수정하기 위해 모든 스트림 스위치에 대해 디코더를 다시 시작하며 최대 3초가 걸릴 수 있습니다. |  |
| 삼성 갤럭시 |  | SampleMediaPlayer 앱을 설치할 수 없습니다. | 보다 일반적인 ARM v7 칩셋 대신 ARM v6를 사용합니다. FP/AIR은 이 장치를 지원하지 않습니다. |  |
| Xom | 테그라 | 전환을 위해 몇 개의 프레임이 드롭됩니다. 디코더가 다시 시작되지 않습니다. | OMXAL 제한. |  |

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
