---
title: Android용 TVSDK 1.4 릴리스 정보
description: Android용 TVSDK 1.4 릴리스 정보에서는 TVSDK Android 1.4의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---


# Android용 TVSDK 1.4 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 1.4 릴리스 정보에서는 TVSDK Android 1.4의 새로운 기능 또는 변경된 기능, 해결되고 알려진 문제 및 장치 문제를 설명합니다.

## 새 기능 {#new-features}

**버전 1.4.43**

**HTTPS를 통한 안전한 광고 로딩**

Adobe Primetime은 HTTPS를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

**MediaPlayer 클래스의 alwaysUseAudioOutputLatency(boolean val)**

이 매개 변수를 설정하면 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

부울 매개 변수 값을 사용합니다. 값이 `True`이면 클라이언트는 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용합니다.

**버전 1.4.42**

**부분 광고 중단 삽입: 부분적으로 시청된 광고에 대한 추적을 시작하지 않고 광고 중간에 참여하는**
TV와 유사한 경험입니다.
예:사용자는 3개의 30초 광고로 구성된 90초 광고 중단의 중간(40초)에 참여합니다. 이것은 10초 동안 2차 광고 뒤에 있습니다.
* 나머지 기간(20초) 동안 두 번째 광고가 재생되고 세 번째 광고가 재생됩니다.
* 부분 재생(두 번째 광고)에 대한 광고 추적기는 실행되지 않습니다. 세 번째 광고에 대한 추적기가 실행됩니다.

**버전 1.4.41**

새로운 기능이 없습니다.

**버전 1.4.40**

새로운 기능이 없습니다.

>[!NOTE]
>
>1.4.39 이전 버전을 사용하고 있는 경우 API를 변경할 필요가 없습니다.

**버전 1.4.39**

* TVSDK는 VHL 2.0.1으로 인증되고 VHL과 Nielsen이 함께 2.0.1.
* Android TVSDK가 새 Akamai 호스트 `primetime-a.akamaihd.net`에서 CRS 요청을 하도록 업데이트되었습니다.
* 새로운 호스트 이름 구성은 HTTP 및 HTTPS(SSL) 모두를 통해 보다 큰 규모로 CRS 에셋 제공을 제공합니다.
* TVSDK는 Android Oreo 릴리스를 지원합니다.
* 여러 개의 기회 감지기 등록을 지원하기 위해 `AdClientFactory` 클래스에 새 함수가 추가되었습니다.

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   이렇게 하면 PlacementOpportunityDetector 배열이 반환됩니다. 이제 여러 개의 기회 탐지기를 등록할 수 있습니다. 예를 들어 초기 광고 종료 기능의 경우 광고 삽입에 대한 두 개의 기회 감지기(광고 조기 종료에 대해 한 개)가 필요했습니다. 이 새로운 기능은 DefaultAdvertisingFactory를 사용하지 않고 직접 AdvertisingFactory를 구현한 경우에만 영향을 주도록 구현해야 합니다. 기존 비헤이비어를 가져오려면 createOpportunityDetector() 함수와 같이 단일 Opportunity Detector를 만들고 배열에 넣고 반환합니다.

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
>1.4.39 이전 버전을 사용하고 있는 경우 API를 변경할 필요가 없습니다.

**버전 1.4.36**

Android에서 내용 건너뛰기 버그 수정.

**버전 1.4.35**

* **네트워크 광고 정보**

   이제 TVSDK API는 제3자 VAST 응답에 대한 추가 정보를 제공합니다. 광고 ID, 광고 시스템 및 VAST 광고 확장은 광고 자산의 networkAdInfo 속성을 통해 액세스할 수 있는 NetworkAdInfo 클래스에서 제공됩니다. 이 정보는 **해자 분석**&#x200B;과 같은 다른 광고 분석 플랫폼과 통합하는 데 사용할 수 있습니다.

**버전 1.4.31**

**CRS 광고에 대한 다중 CDN 지원**
* 기본적으로, 모든 코드 변환된 에셋은 Akamai의 Adobe 소유 CDN에 호스팅됩니다. 최신 릴리스를 통해 Adobe CRS(Creative Repackaging Service)는 고객이 지정한 대로 트랜스코딩된 크리에이티브를 여러 CDN에 업로드할 수 있는 기능을 제공합니다.
* 기본 URL이 사용되지 않을 때 최종 CRS 크리에이티브 URL을 지정할 수 있도록 새 API가 TVSDK에 추가됩니다. 이러한 새로운 API를 사용하는 방법에 대해 알아보려면 설명서를 참조하십시오.

**버전 1.4.18**
Primetime Android TV SDK는 이제 VPAID 2.0 Javascript 크리에이티브를 지원하므로 인터랙티브한 인스트림 광고 경험을 제공할 수 있습니다. VPAID 2.0에 대한 자세한 내용은 [VPAID 광고 지원](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)을 참조하십시오.

**버전 1.4.17**

AC-3 5.1은 Amazon FireTV에서만 지원됩니다.

**버전 1.4.11**

* **광고 폴백, 광고 선택 로직의 데이지 체인(폴백 규칙** 이 활성화된 VAST 광고(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용하려고 합니다. 폴백 동작의 일부 측면을 구성할 수 있습니다.

자세한 내용은 VAST 및 VMAP 광고](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)에 대한 광고 폴백을 참조하십시오.[

* **버전 1.5로 업데이트된 비디오 하트비트 라이브러리(VHL)**
   * 비디오 시작 및/또는 비디오/광고/장 시작을 컨텍스트 데이터로 포함하는 메타데이터 전송
   * 네트워크 트래픽 감소 - 하트비트가 평균 감소하며 크기가 작음

**버전 1.4.7**

* **온-프레미스 개인화**&#x200B;지원 Adobe Indification Server의 온-프레미스 설치를 지원하여 클라이언트의 개별화 요청을 다른 종단점으로 가져가도록 사용자 지정합니다.

**버전 1.4.6**

* **샘플 AES 암호화(Flash Player 버전 17.0.0.134 필요)**샘플 기반 AES 암호화가 지원됩니다.

**버전 1.4.2**

* **비디오 하트비트 라이브러리(VHL)가 버전 1.4.0.1으로 업데이트**

   * Adobe Analytics Video Essentials를 사용하여 다른 SDK 또는 플레이어에서 다양한 분석 사용 사례를 번들로 제공하는 기능을 추가했습니다.
   * trackAdBreakStart 및 trackAdBreakComplete 메서드를 제거하여 광고 추적을 최적화했습니다. trackAdStart 및 trackAdComplete 메서드 호출에서 광고 나누기가 유추됩니다.
   * 광고를 추적할 때 재생 헤드 속성이 더 이상 필요하지 않습니다.

* **Nielsen SDK**&#x200B;통합 이제 TVSDK는 사용자 정의 통합 없이 Nielsen SDK로 사용자 추적 정보 전송을 지원합니다.

**버전 1.4.0**

* **대체 컨텐츠** 교체를 통한 일시 중단 신호 1.4 TVSDK 업데이트의 일부로 TVSDK는 또한 선형 컨텐츠에 대한 지역적 일시 중단 시작 및 복귀를 지원합니다. 이제 TVSDK는 두 개의 매니페스트 파일을 동시에, 기본 파일을, 그리고 다른 버전으로 처리할 수 있으므로, 원래의 프로그래밍 대신 대체 프로그램이 보여지는 경우에도 정전 신호를 모니터링할 수 있습니다.

* **C3 광고 제거/** 바꾸기 이제 C3 창에서 나오는 VOD(Video-On-Demand) 자산에 새로운 광고를 동적으로 삽입하는 데 별도의 준비 작업이 필요하지 않습니다. 이제 TVSDK에서 사용자 지정 컨텐츠 범위를 제거하고 새 광고를 동적으로 삽입할 수 있는 API를 제공합니다. 이 강력한 새로운 기능은 브로드캐스트 중에 라이브/선형 컨텐츠가 실행되고 에셋을 &quot;정리&quot;하는 데 적절한 시간 없이 on-demand 컨텐츠로 사용하기 위해 즉시 축소되는 경우에도 유용합니다.

* 인터페이스 PlaybackEventListener에는 onReplaceMediaPlayerItem이라는 새 메서드가 있으며, 이 메서드는 새 이벤트 `ITEM_REPLACED`에 대해 수신하는 데 사용할 수 있습니다. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스를 교체할 때마다 전달됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.
* AdClientFactory에는 다음과 같이 여러 개의 기회 감지기에 등록할 수 있도록 새 함수가 클래스에 추가되었습니다.

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

## 1.4 {#tvsdk-changes}에 대한 TVSDK 변경 사항

* PlaybackEventListener 인터페이스에는 새 이벤트인 ITEM_REPLACED를 수신하는 데 사용할 수 있는 onReplaceMediaPlayerItem이라는 새 메서드가 있습니다. 이 이벤트는 MediaPlayer에서 MediaPlayeritem 인스턴스를 교체할 때마다 전달됩니다. 이 PlaybackEventListener를 구현하는 클라이언트 응용 프로그램은 이 새 메서드를 구현하거나 재정의해야 합니다.

* AdClientFactory에는 다음과 같이 여러 개의 기회 감지기에 등록할 수 있도록 새 함수가 클래스에 추가되었습니다.

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

예를 들어 초기 광고 종료 기능의 경우 광고 삽입에 대한 두 개의 기회 감지기(광고 조기 종료에 대한 측정기 하나)가 필요합니다.

이 새 함수를 재정의하려면 단일 Opportunity Detector를 만들고 배열에 넣고 반환합니다.

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4 {#device-certification-and-support-in}의 장치 인증 및 지원

>[!NOTE]
>
>다음은 TVSDK에서 지원되지 않는 **기능입니다.**
>
>* 모든 플랫폼 또는 버전에서 슬로우 모션 제작
>* 라이브 트릭 플레이


**버전 1.4.43**

TVSDK 1.4.43은 Android 6.0.1/ 7.0 및 8.1(Oreo)의 Android 디바이스에서 인증되었습니다.

* **버전 1.4.23:**

   * TVSDK 1.4.23은 Android N 기반의 Android 디바이스에서 인증되었습니다.

* **버전 1.4.18:**

   * Primetime은 Amazon Fire TV의 인증을 받았습니다.
   * VPAID 2.0은 Android 4.0 이상의 디바이스에서만 지원됩니다.

## 1.4 {#resolved-issues-in}에서 해결된 문제

>[!NOTE]
>
>CRS를 사용하는 모든 TVSDK 고객은 iOS 및 Android 기반의 TVSDK 1.4.39 또는 최신 버전으로 업그레이드할 것을 적극 권장합니다. 이 업그레이드는 기존 앱 구현에 대한 드롭인 교체입니다. 업그레이드 후 프록시 도구의 CRS 크리에이티브 URL 요청(예: Charles)을 확인하여 경로의 버전이 버전 3.1을 반영하는지 확인합니다. 예:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**버전 1.4.43**

* Ticket #27143 - FireTV 장치에서 5.1 오디오 트랙을 재생할 수 없습니다.

   * 이제 TVSDK에서 FireTV 장치에서 AC3 오디오를 재생할 수 있습니다. 재생은 항상 스테레오로 이루어집니다.

* 티켓 #33902 - HTTPS를 통한 안전한 광고 전달

   * Adobe Primetime은 https를 통해 primetime 광고 서버 및 CRS에 대한 첫 번째 호출을 요청하는 옵션을 제공합니다.

* 티켓 #34493 - 블루투스 오디오 지연

   * 설정되면 오디오 타임스탬프 계산에서 오디오 출력 지연을 사용할 수 있는 `alwaysUseAudioOutputLatency`을 MediaPlayer 클래스에 추가했습니다.

* 티켓 #34949 - 새로운 버전의 비디오 하트비트 라이브러리(VHL)가 통합되었습니다.

**버전 1.4.42 (1791)**

* Zendesk #33719:FireTV 4k 적응형 비트 전송률이 느리게 조절됩니다. FireTV 4K 장치용 ABR 지원을 추가했습니다.
* Zendesk #33338: resetDRM은 응용 프로그램의 모든 데이터를 지웁니다.  비-TVSDK 스레드에서 예외가 발생하여 TVSDK 작업 큐가 채워지는 경우를 추가로 처리했습니다.

**버전 1.4.41 (1776)**

* Zendesk #33002 - Fire TV에서 TVSDK와 함께 사용 가능한 에셋 데이터 Companion 데이터를 List &lt;AdBannerAsset> 및 AdAsset::id로 반환하는 새 클래스 AdBannerAsset을 구현했습니다. 이제 id는 길이가 아닌 문자열입니다.
* Zendesk #32821 - Android Primetime 플레이어는 WWE에 대한 PTS(프레젠테이션 타임스탬프)가 발생하면 중지됩니다. 이 문제는 이번 릴리스에서 해결되었습니다.
* Zendesk #33572 - VideoAnalytics공급자 광고 시작 충돌. VideoHeartbeat.jar의 VHL+Nielsen 공동 SDK 버전의 올바른 조합을 사용하여 이 문제를 수정했습니다.
* Zendesk #33355 - Fire TV:15초 발행물 스크러빙. TV SDK 측에서 수정한 사항은 없고, 고객은 본 행사를 본 최종 사용자 및 제3자에서 확인하고 있습니다.

**버전 1.4.40 (1764)**

* Zendesk #33068 - 새 장치의 Amazon 립싱크 문제 립싱크 문제가 이번 릴리스에서 수정되었습니다.
* Zendesk #32215 - Android TVSDK 1.4.38 보안 문제 `[Hotlist]`. 최신 OpenSSL-1.1.0 및 curl-7.55.1으로 업데이트되었습니다.
* Zendesk #32920 - 광고 중단 내 빈 화면 및 광고 중단 완료 없음 VPAID 컨테이너가 중단 상태로 전환되고 Facebook VPAID 광고가 단일 \&amp;lt;AdParameters\&amp;gt;광대한 노드.

**버전 1.4.39 (1744)**

* Zendesk #28976 - 라이선스 요청은 1초 이상 걸립니다. POST을 사용하는 DRM 라이센스 요청 호출이 실행 중일 때 Curl은 추가 &quot;예상:100-continue&quot; 헤더. TVSDK에서 &quot;예상:&quot; 헤더가 제거되었습니다.
* Zendesk #27707 - CSAI 환경에서는 CUE IN 마커를 사용하여 일찍 돌아오거나 컨텐츠로 돌아갈 수 없습니다. 여러 기회 생성기에 대한 지원을 제공했습니다.

**버전 1.4.38 (1722)**

* Zendesk #21590 - 최신 원본 빌드의 비디오 성능 및 추적

API의 복잡성을 줄여 VideoHeartbeatsLibrary 구현의 장벽을 줄이기 위해 TVSDK에 VHL 2.0을 통합 및 인증합니다.

* Zendesk #29688 - Android O 베타 고객을 지원합니다.

새로운 Android 베타 릴리스에 대한 TVSDK 지원

**버전 1.4.36 (1713)**

* Zendesk #27392 - Android에서 컨텐츠 건너뛰기

암호 해독을 수용하기 위해 Android TVSDK가 비프레임 컨텐츠의 바이트 범위를 16바이트로 잘못 확장했습니다. 확장 작업은 Iframe 스트림에 필요하지만 비프레임 스트림에는 필요하지 않습니다.

**버전 1.4.34 (1702)**

* Zendesk #27638 - cURL INet 객체의 누수

cURL 연결에 사용된 공유 관리자 및 DNS 캐시를 유지하는 동안 Posix cURL INet 개체가 새어 나갔습니다.

이 문제는 INet 해체기에서 Posix cURL INet 객체를 삭제하여 해결되었습니다.

**버전 1.4.33 (1694)**

* **OpenSSL 라이브러리**

OpenSSL 라이브러리가 OpenSSL 버전 1.0.2j로 업데이트되었습니다.

* Zendesk #21701 - 표준화된 URL 대신 1401 CRS 요청에 대한 원래 크리에이티브 URL을 전송합니다.
이 문제는 원래 크리에이티브 URL을 전송하여 해결되었습니다.

* Zendesk #25023 - 비디오 재생 시간 단축:비디오 고정, 화면 깜박임
이 문제는 CenturyLink 셋톱 박스 장치의 최대 비디오 형식 크기를 설정하여 해결되었습니다.

* Zendesk #27460 - 새 Akamai 계정은 POST cdn 요청을 처리할 수 없습니다.
코드가 업데이트되어 `cdn.auditude.com` 광고 요청이 POST 대신 GET이 되도록 했습니다.

* Zendesk #28245 - 앱이 백그라운드에서 전경으로 이동될 때 재생 상태가 올바르게 통보되지 않습니다.
응용 프로그램이 전경으로 돌아갈 때 재생 또는 일시 정지하도록 재생 상태를 올바르게 복원하여 이 문제를 해결했습니다.

**버전 1.4.32 (1682)**

* Zendesk #25779 - TVSDK에서 발견된 보안 취약점
WebView에서 JavaScript를 사용할 경우 Android 4.2 이하에는 보안 취약점이 있습니다. OS 4.2 이하를 실행하는 장치에 대해 TVSDK로 WebView를 사용할 수 없습니다. 이렇게 하면 이러한 장치에서 TVSDK의 VPAID 광고 사용이 비활성화됩니다.

* Zendesk #26890 - Ref 처리 시 화면 상태(켜기/끄기) 문제 플레이어
Adobe 비디오 엔진(AVE)이 일시 중단 상태에서 다시 시작되면 DefaultMediaPlayer가 해당 상태를 업데이트하지 않습니다. 따라서 AVE가 재생 중 상태인 경우에도 DefaultMediaPlayer는 일시 중단 상태로 유지됩니다. AVE로부터 재생 상태를 받을 때 DefaultMediaPlayer의 현재 상태가 일시 중단되어도 DefaultMediaPlayer 상태를 PLAYING으로 설정하여 이 문제가 해결되었습니다.

**버전 1.4.31 (1675)**

* Zendesk #21974 - Null 개체로 인한 예외
   * AdIndex는 null일 때 증가되는 경우가 거의 없습니다. 이는 프리롤 adBreak에 대해 수신한 잘못된 API 호출 때문일 수 있습니다. 이러한 예외를 피하도록 데이터 유형을 수정했습니다.

* Zendesk #24714 - 외부 로깅 해제
   * 외부 로깅(logging)을 끄도록 TVSDK를 업데이트했습니다.

* Zendesk #24488 - Fire TV의 AV 동기화 문제
   * AV 디코더 스레드 처리를 개선하여 수정했습니다. 특히 입력 또는 출력 프레임 큐가 수정될 때마다 프레임의 내용 유형에 맞는 디코더 스레드가 실행됩니다.

* Zendesk #26551 - CRS 오류 수정
   * 요청이 HEAD(http head)인 경우 콘텐츠가 비어 있으므로 해당 콘텐츠를 읽을 필요가 없습니다. read()를 호출하면 이전 Android(4.0.x)가 정지되지만 read()를 호출하면 최신 Android 반환 올바른 값(-1)이 반환됩니다. 이에 따라 코드가 &quot;head&quot;에 대한 컨텐츠를 읽지 않도록 변경되었습니다.

* TrickPlayManager 액세스 시 Zendesk #26696 Null 포인터 예외
   * TrickPlayManager 개체를 사용하기 전에 null이 아닌지 확인하여 수정했습니다.

**버전 1.4.30 (1659)**

* Zendesk #22675 Asset 지속 시간은 라이브/선형 스트림에 대해 업데이트되지 않습니다.
이 문제는 라이브 및 선형 스트림의 자산 지속 시간을 제공하는 PTVideoAnalyticsTrackingMetadata에 새 API, assetDuration을 제공하여 해결되었습니다.

* 채널 전환 시 TVSDK에서 #25853 메모리 누수
파일을 다운로드하는 동안 MediaPlayer를 재설정하거나 해제할 때 파일 읽기 버퍼 누수가 발생하는 문제가 해결되었습니다.

**버전 1.4.29 (1653)**

* Zendesk #21200 - 앱이 백그라운드에 있을 때 플레이어가 일시 중단된 상태에서 복구되지 않음
스트림 스위치가 신호를 받은 후 플레이어가 일시 중단되었을 때 해상도를 통해 이전 위치로 복원하는 대신 플레이어가 일시 중단 상태에서 복구할 때 플레이어가 스트림 스위치를 수행할 수 있습니다.

* Zendesk #23412 - 광고 분리의 마지막 3s 내에서 광고를 클릭하면 플레이어에 검정색 상자가 표시됩니다.
이 문제는 Zendesk과 동일한 #21200.

* Zendesk #23616 - 광고 나누기가 너무 먼 미래를 찾습니다.
광고 삽입 유형(삽입/바꾸기)에 따라 TVSDK는 광고 중단점을 결정하는 데 광고 기간이 계산에 사용되는지 여부를 결정합니다.

* Android TV STB에서 #25078 - TVSDK DRM 메모리 누수
DRM 어댑터 개체의 메모리 누수가 찾아서 수정되었습니다.

* Zendesk #25067 - Crash in VideoEngine타임라인
개체가 올바르게 정리되지 않고 개체가 제거된 후에 이벤트가 호출되었기 때문에 이러한 문제가 발생합니다. null 예외를 방지하기 위해 검사를 추가하여 문제를 해결했습니다.

* Zendesk #25352 - 사용자 지정 HTTP 헤더 설정
이 문제는 TVSDK의 허용 목록에 새 사용자 정의 헤더를 추가하여 해결되었습니다.

* Zendesk #25617 - 라이브 스트림 PTS 롤오버 때문에 플레이어 불연속성 및 메모리 충돌이 발생했습니다.
이 문제는 롤오버가 세그먼트 중간에 발생할 때 파편화된 HTTPStreamer에서 PTS 롤오버 처리를 추가하여 해결되었습니다.

**버전 1.4.28 (1637)**

* Zendesk #23618 - 광고 정책이 참조되기 전에 광고 중단 이벤트 실행
adForument로 인해 광고를 건너뛸 때 AD_BREAK_START 및 AD_START 이벤트를 실행하지 않아 이 문제가 해결되었습니다. AD_BREAK_SWITCHED 이벤트가 대신 전송됩니다.

**버전 1.4.27 (1631)**

* Zendesk #23174 - 비디오 크기 조정 시 성능 문제
이 문제는 TV SDK가 MediaPlayerView의 SurfaceHolder.setFixedSize()에 액세스할 수 있는 새 API, MediaPlayerView.setSurfaceFixedSize()를 증명하여 해결되었습니다.

* Zendesk #24450 - TVSDK에서 광고 요청 복제
이 문제는 경과된 시간이 2배가 아닌 길이로 변환되어 이 문제가 해결되었습니다.

**버전 1.4.26 (1627)**

* Zendesk #21436 - OpenSSL 라이브러리 업데이트 1.0.2h OpenSSL 라이브러리를 OpenSSL 버전 1.0.2h로 업데이트했습니다.
* Zendesk #23825 - Android 쿠키에 대한 지원을 제공함으로써 쿠키가 콜백에 포함되지 않습니다.

**버전 1.4.25 (1620)**

* Zendesk #22900 - Live Adobe Primetime DRM 스트림이 Android 참조 플레이어에서 재생되지 않습니다.
메모리 할당 문제가 수정되었습니다.
* Zendesk #23176 - VPAID 광고를 재생하려고 할 때 애플리케이션이 충돌합니다.
애플리케이션이 VPAID 광고를 렌더링할 사용자 지정 광고 보기를 만들지 않으므로 충돌이 발생했습니다. 이 문제는 사용자 지정 광고 보기가 없을 때 광고 서버 응답에서 VPAID 광고를 무시함으로써 해결되었습니다.

* Zendesk #23153 - SampleAES DRM Stream - TVSDK 참조 플레이어에서 재생 지연
이 문제는 Zendesk #22900.

**버전 1.4.24 (1612)**

* Zendesk #20784 - Analytics:라이브 비디오 전환을 위한 콘텐츠 트리거가 완료됩니다.
이 문제는 라이브/선형 비디오 추적 세션 중에 API(trackVideoComplete)를 추가하여 컨텐츠 완료를 수동으로 트리거함으로써 해결되었습니다.

* Zendesk #21977 VideoEngineTimeline Crash during placeAdBreak/acceptAd 작업
   * 이 문제에서는 다음 라이브러리가 업데이트되었습니다.
      * Adobe Mobile 라이브러리를 버전 4.10.0으로 변환
      * VHL 라이브러리를 버전 1.5.6
      * VHL-Nielsen 라이브러리 - 버전 1.6.7

이 문제는 승인된 광고 목록에 광고를 추가하기 전에 null 검사를 추가하여 해결되었습니다.

* Zendesk #22313 Amilogic 칩셋이 설치된 STB의 비트 전송률은 1.2M을 초과하지 않습니다.
이 문제는 미디어 코덱을 미리 로드하고 Amilogic 칩셋 장치에 대한 매끄러운 스위치를 비활성화하여 해결되었습니다.

* Zendesk #19520 TVSDK 플레이어에서 재생되지 않는 샘플 AES HLS 에셋
이 문제는 샘플 AES 암호화된 HLS 스트림에 대한 여러 PMT 설명자를 처리하여 해결되었습니다.

**버전 1.4.23 (1602)**

* Zendesk #18852 - CRS 규칙을 기반으로 크리에이티브 선택 로직 업데이트
이 문제는 JSON 구성 파일을 추가하여 크리에이티브 선택 우선 순위를 지정함으로써 해결되었습니다.

* Zendesk #20861 - Android N
이 릴리스는 Android N에서 실행되는 응용 프로그램에서 더 이상 액세스할 수 없는 Android 플랫폼 기본 라이브러리를 직접 사용하는 기능을 제거하여 Android N을 지원합니다.

* Zendesk #21018 - Android N 충돌
ZD# 20861과 동일한 해상도입니다.

* Zendesk #21266 - VideoEngineAdapter가 Invalid_Key 오류 시 충돌합니다.
Invalid_Key 오류는 AVE의 설명을 포함하지 않으므로 텍스트를 구문 분석하면 NPE가 됩니다. 설명을 구문 분석하기 전에 onError 중에 설명을 null 검사로 추가하여 문제를 해결했습니다.

* Zendesk #22286 - 기본 라이브러리가 메모리 읽기 키/조각을 할당하여 충돌을 발생시킵니다.
여러 개의 키를 동시에 사용하여 매니페스트를 로드하려고 할 때 Android에서 발생한 이 충돌 문제가 수정되었습니다.

**버전 1.4.22 (1581)**

* Zendesk #17236 - DRM을 사용하는 HLS 비디오의 재생 시간이 불안정합니다.
오디오 세그먼트 시작 시간이 비디오 세그먼트 시작 시간과 일치하지 않는 LBA 스트림과의 시간 이동 시간이 수정되었습니다.

* Zendesk #17680 - 선택 영역 안드레도 상자에서 비디오 재생이 멈춥니다.
이 장치의 비디오 디코더에서는 출력 버퍼에서 비디오 프레임을 대기열에 넣어도 출력 시간 증가가 크게 유지되며 이 출력 타임스탬프가 높게 유지되는 경우가 있습니다. 이 문제는 플레이어가 동일한 프로필을 다시 시도하거나 다른 프로필을 선택하도록 강제하지 않는 *비디오 프로필이 지원되지 않음* 오류를 반환하여 해결되었습니다.

* Zendesk #19074 - FWD 및 REW 트릭 재생 중 비디오 고정
이 문제는 TRICKPLAY_ENDED_DUE_TO_ERROR를 추가하여 Trickplay가 종료되었고 복구할 수 없는 오류로 인해 비디오가 일시 중지되었음을 응용 프로그램에 통보함으로써 해결되었습니다.

* Zendesk #19574 - TVSDK에서 DRM 또는 비 DRM 컨텐츠에 대한 M3U8 응답 데이터를 반환하지 않습니다.
이 문제는 다음과 같은 방법으로 해결되었습니다.

* Zendesk #19986 - Android TV와 같은 특정 장치에 대한 OP 비헤이비어가 끊김
* 조건에 FILE_NOT_FOUND 오류를 추가하는 중입니다.
* *파일을 찾을 수 없음* 오류에서 오류가 발생하면 URL과 응답을 오류 설명에서 분리하는 것이 좋습니다(응답을 사용할 수 있는 경우).
NVidia shield OP 지원에 의해 도입된 논리 오류가 수정되었습니다. NVidia가 아닌 장치의 경우 표시 유형을 알 수 없는 경우에도 표시 보안 플래그를 신뢰합니다.

* Zendesk #20549 - 오래된 재생 목록 처리. 이전 가져오기에서 새 세그먼트를 받지 못할 경우 라이브 매니페스트 업데이트 사이의 간격을 예상 세그먼트 기간의 절반 수준으로 줄여 이 문제가 해결되었습니다.

* Zendesk #20742 - FireTV에서 라이브 컨텐츠를 재생할 때 메모리 사용이 계속 증가하는 것 같습니다.충돌을 일으키는 이유는 제한에 도달한 JNI 객체 참조 테이블이 원인입니다. 디코더를 다시 시작하는 동안 생성된 MediaFormat 객체에 대한 참조를 삭제하여 이 문제가 해결되었습니다.

* Zendesk #21125 - 라이브/선형 광고 일찍 중단(CSAI)에서 돌아갑니다. 플레이어에서 기회 탐지기에 스플릿을 사용하여 광고 큐에 스플리스를 등록하는 경우 광고 중단 동안 플레이어에서 기본 컨텐츠로 돌아갈 수 있도록 하는 기능을 추가했습니다.

* Zendesk #21334 - TVSDK 및 제3자 광고 요청에 대한 요청 시간 초과 값입니다. 광고 호출에 대한 전역 시간 제한을 활성화하는 adRequestTimeout 설정이 AdvertisingMetadata에 추가되었습니다.

**버전 1.4.21 (1566)**

* Zendesk #17781 - ADB 화면 캡처가 더 이상 작동하지 않음
화면 캡처를 허용하는 DefaultMediaPlayer.create(Context, boolean secureSurface) API를 추가하여 이 문제를 해결했습니다.
화면 캡처를 허용하려면 secureSurface에 대해 false를 전달합니다.
중요:제작 설정에서 이 화면 캡처 기능을 활성화하지 않는 것이 좋습니다.

* Zendesk #19074 - FWD 및 REW 트릭 재생 중 비디오 고정
재생 백그라운드에서 trickPlay가 정지될 수 있을 때 발생하던 다음 문제가 해결되었습니다.

* Zendesk #19532 - 캡션 닫기가 순서대로 표시되지 않습니다.
   * FHS는 trickplay를 시작하지만 첫 번째 iframe 세그먼트에 프레임이 없습니다.
   * iframe 세그먼트를 다운로드하는 동안 FHS에서 오류 조건을 만나면 trickplay에서 종료되고 재생을 일시 정지합니다.
   * Android MediaCodec 구현은 모든 입력/출력 버퍼를 플러시하라는 요청을 받는 동안 입력 큐 가용성을 항상 기다립니다.
이 문제는 겹치는 여러 큐가 &quot;위로 스크롤&quot;하는 것처럼 표시되도록 WebVTT 큐의 순서를 반전하여 해결되었습니다.

* Zendesk #19574 - TVSDK가 DRM 또는 비 DRM 컨텐츠에 대한 M3U8 응답 데이터를 반환하지 않습니다.
PTMediaPlayerItem.prepareToPlay에서 매니페스트 파일을 처음 로드할 때 로드가 실패할 경우 TVSDK는 애플리케이션에 실패 응답 본문을 보고하지 않습니다.
이 문제는 TV SDK가 오류 응답을 응용 프로그램에 보고하도록 허용하여 해결되었습니다.

* Zendesk #19701 - SAP/Dis연속성을 사용한 재생 중단
연결이 끊어진 상태에서 오디오와 비디오가 정렬되지 않을 때 플레이어가 고정됩니다.

* 버그 #PTPLAY-11162 - OpenSSL 라이브러리 업데이트가 1.0.2f 버전으로 해결되었습니다.

**버전 1.4.20 (1546)**

* Zendesk #17384 - 기능 요청:AAC 재생을 위한 ID3 메타데이터 지원
AAC 미디어의 ID3 태그에 대한 지원은 버전 1.4.20부터 Android용 TVSDK에서 제공됩니다.

* Zendesk #18358 - 동기화 중단 없는 비트 전송률 스위치에서 플레이어가 멈춥니다.
이 문제는 ABR 연결 에지 사례를 적절하게 처리하여 해결되었습니다.

* Zendesk #19232 - TVSDK 1.4.18을 사용하는 앱이 이전 Amazon OS 버전 4에서 이상하게 작동합니다.
이 문제는 Android Webview를 지원하지 않는 장치와의 충돌을 방지하기 위해 TVSDK 플레이어 초기화 프로세스에서 숨겨진 웹 보기 생성을 제거하여 해결되었습니다.

* 적응형 비트 전송률 전환이 발생할 때 Zendesk #19585 - 슬로우 모션 재생
ABR 스위치 중에 새 프로파일의 오디오 샘플 속도가 현재 프로파일과 다른 경우 재생이 빨라지거나 느립니다. 이는 비디오 발표자에게 오디오 형식이 변경되었다는 알림을 받지 않기 때문입니다.
이 문제는 알림 플래그가 올바른 위치에 설정되어 있는지 확인하여 해결되었습니다.

* Zendesk #19683 - SAP DAI 재생 - 몇 초 동안 오디오가 없습니다.
TVSDK의 논리에서 두 변환 세그먼트의 타임스탬프를 비교할 때 타임스탬프가 항상 0 ms 차이와 일치할 수 없으므로 RENDITION_TIMEOUT_THRESHOLD가 허용되는 값 범위로 사용되었습니다. 간격이 RENDITION_TIMEOUT_THRESHOLD 범위 내에 있는 경우 일치하는 것으로 가정합니다.

RENDITION_TIMEOUT_THRESHOLD가 100ms로 설정되었지만 특정 스트림에 부족한 것으로 발견되었습니다. 이 문제는 RENDITION_TIMEOUT_THRESHOLD를 200ms로 증가시켜 해결되었습니다.

* Zendesk #19699 - TVSDK가 VTT 자막 트랙 간을 전환하지 못함
이 문제는 트랙이 변경될 때 플레이어 덤프 및 매니페스트를 다시 로드하도록 하고 더블바이트 WebVTT 캡션 트랙 이름에 영향을 준 UTF8 문자열 변환 문제를 수정하여 해결되었습니다.

* Zendesk #19717 - CC 옵션 표시 문제
이 문제는 유니코드 문자열을 올바르게 처리하여 해결되었습니다.

* Zendesk #19910 - TIT2 ID3 태그를 찾을 수 없음
이 문제는 ID3 v2.4 문자열 인코딩에 대한 완벽한 지원을 제공하고 ID3 v2.3을 지원함으로써 해결되었습니다.

* Zendesk #20135 - TVSDK가 VOD 컨텐츠에 대해 여러 onComplete를 트리거하고 있습니다.
이 문제는 상태 변경 이벤트의 전체 경우에서가 아니라 적절한 위치에 post_roll_complete 이벤트 리스너를 추가하여 해결되었습니다.

**버전 1.4.19 (1521)**

* Zendesk #4180 - TVSDK가 HDCP를 적용하지 않습니다.
   * 이 티켓에 대한 부분 수정이며 NVidia shield 장치의 문제만 해결합니다.
HDCP 상태를 동적으로 추적하려면 Nvidia Shield에서 올바르게 구현된 HDCP 감지 API를 사용해야 합니다.

* Zendesk #18358 - 동기화 불연속성이 있는 비트 전송률 스위치에서 TVSDK가 중지됩니다.
   * 이 문제는 PTS 불연속성을 탐지하기 위한 새로운 경고를 추가하고 PTS 검사를 강제로 수행하여 모든 ABR 스위치에 대한 올바른 세그먼트 검색을 다시 실행함으로써 해결되었습니다.
고정을 수정하려면 mediaPlayer.setCustomConfiguration 메서드에 대한 호출에는 forcePTSCheckForABR을 인수로 포함해야 합니다.

* Zendesk #19038 - Asus Zenpad 10에는 라이브 스트림이 없습니다.

   이 문제는 런타임에 함수를 쿼리하지 않도록 미디어 코덱을 미리 로드하여 해결되었습니다.

* 다음 문제는 Zendesk과 #19038입니다.
   * Zendesk #19483 - TVSDK가 인텔 플랫폼에서 충돌하고 있습니다.
   * Zendesk #19171 - Android 5.0이 있는 Asus 메모 Pad 7에서 충돌이 발생합니다.

**버전 1.4.18 (1503)**

* Zendesk #3324 - Primetime 광고 보고는 VMAP에 광고 미디어가 없을 때 광고 브레이크 추적을 하지 않습니다.
광고 브레이크가 비어 있으면 광고 브레이크 시작 및 전체 추적 이벤트가 핑되지 않았습니다. 이 문제는 VMAP AdBreak와 같은 빈 광고 중단에 유효한 AdSource 노 쌍으로 광고 중단 시작 페이지를 전송하여 해결되었습니다.

* Zendesk #18229 - SetCCVisability(VISIBLE)는 MediaPlayer.reset() 호출 후 무시됩니다.
이 문제는 setCCVisibility(Visibility.INVISIBLE)을 추가하여 해결되었습니다.를 다시 설정합니다.

* Zendesk #18328 - 60FPS의 컨텐츠를 위한 Amazon Fire TV 2세대 장치의 드롭된 프레임 문제
이 문제는 절전 시간 결정을 위한 인코딩된 FPS를 적용하고 더 잘 인코딩된 FPS 예측 논리를 적용하여 해결되었습니다.

**버전 1.4.17 (1472)**

* Zendesk #2231 - MediaPlayerNotification에서 사용할 수 없는 매니페스트를 가져올 때 오류가 반환되었습니다.
구문 분석 오류가 있는 경우 매니페스트의 응답 본문을 포함하여 이 문제가 해결되었습니다.

* Zendesk #17703 - VideoEngineView는 비디오 재생 중에 스크린샷을 방지하지 않습니다.
setSecure 메서드는 API 17 이후 사용할 수 있었지만 API 17은 4.2, 4.2.1 및 4.2.2을 적용하므로 예외를 throw할 사람이나 장치별 것인지를 알 수 없습니다. 이 문제는 VideoEngineView.setSecure를 try catch 절에 래핑하여 해결되었습니다.

* Zendesk #17919 - 컨텐츠 검색으로 하트비트 오류가 발생합니다.
프리롤 후 검색을 시작할 때 생성된 하트비트 호출의 결과로 잘못된 입력 데이터 위치 오류가 발생했습니다. 이 문제가 해결되었습니다.

**1.4.16a** (1454a)

* Zendesk #18215 - 일부 AES 스트림을 로드할 수 없습니다.
이 문제는 AES 키를 로드하기 전에 프로필 DRM 메타데이터 크기를 확인하여 해결되었습니다.

**버전 1.4.16 (1454)**

* Zendesk #3875 - 재생 중 탭 충돌
이제 TVSDK가 curl 대신 httpurconnection을 직접 사용하기 때문에 CRS용 Auditude에 대한 OKHTTP의 종속성을 되돌립니다. 다른 JNI 호출을 하기 전에 예외를 지워 문제를 해결했습니다.

* Zendesk #4487 - 컨텐츠 선형 채널 추적
선형 스트림 재생 세션 중에 비디오 하트비트 추적기를 다시 초기화하여 문제가 해결되었습니다.

* Zendesk #17919 - Android - 컨텐츠 검색 시 하트비트 오류 발생
장에 탐색이 있을 때 하트비트가 오류 상태에 있을 때 발생하는 문제가 해결되었습니다.

* Zendesk #18053 - Marshmallow에서 Adobe Primetime 충돌
TVSDK 라이브러리가 YUV -> RGB 색상 변환을 수행하는 네온 코드를 사용할 때 TVSDK가 Android M OS에서 충돌했습니다. 이 문제는 네온이 아닌 버전의 코드를 사용하여 이 문제를 일으키는 함수를 업데이트하여 해결되었습니다.

* Zendesk #18072 - Android M - 애플리케이션 충돌
프로파일과 수준이 지원되는지 확인할 때 MediaCodecList 및 MediaCodecInfo API를 호출할 때 충돌이 발생합니다. 코덱정보가 필요한 경우에만 이러한 API를 호출할 수 있도록 미리 모든 코덱정보를 로드하여 일시적으로 문제가 해결되었습니다.

* Zendesk #18074 - Android 6.0의 Nexus에서 아랍어 자막이 작동하지 않음
Android에 대한 CTS 글꼴 맵 지원을 제공하여 문제가 해결되었습니다.

**버전 1.4.15 업데이트(1438)**

* Zendesk #17437 - 일부 AES 스트림으로 VOD 컨텐츠 시작 시간이 오래 지연됩니다.
이 문제를 해결하려면 매니페스트에 여러 개의 키가 있는 경우 모든 AES 키를 동시에 다운로드합니다.

**버전 1.4.15 (1435)**

* Zendesk #4278 - ABR(적응형 비트 전송률 변경 시 Android의 문제 발생 상단 상자 설정
최신 Android 미디어 코덱을 사용하여 완벽한 ABR 스위치에 대한 지원을 추가하는 것이 수정되었습니다.

* Zendesk #17063 - mediaPlayer.reset()을 호출하면 비디오 엔진 재설정 오류가 발생합니다.
ErrorEvents를 전달할 때 VideoEngineExceptions의 원본 MediaErrorCode를 포함시키는 문제를 해결했습니다.

* Zendesk #17130 - FireTV에서 표시되는 비트 전송률을 변경할 때 잠깐이지만 눈에 띄는 일시 정지입니다.
(위의 #4278과 동일) 최신 Android 미디어 코덱을 사용하여 연속 ABR 스위치에 대한 지원을 추가하는 문제가 수정되었습니다.

* Zendesk #17666 - 컨텐츠를 다시 시작할 때 추가 광고 마커, 예기치 않은 또는 광고 없음.
VOD(Video-On-Demand) 컨텐츠에서 prepareToPlay를 수행할 때 가상 시간이 아닌 로컬 시간에 초기 검색이 수행되던 문제가 수정되었습니다.

* Zendesk #17437 - 일부 AES 스트림으로 VOD 컨텐츠 시작 시간이 오래 지연됩니다.
여러 키가 매니페스트에 나열될 때 모든 AES 키를 동시에 다운로드할 수 있었습니다.

* Zendesk #17851 - Android TV - ABR 도중 검정 프레임
적응형 재생을 활성화하려면 KEY_MAX_WIDTH 및 KEY_MAX_HEIGHT를 지정하는 문제가 수정되었습니다.

**버전 1.4.14 (1415)**

* Zendesk #3875 - 재생 중에 Tab이 충돌합니다.
충돌을 방지하기 위해 추가 수정이 필요합니다.

* Zendesk #17245 - Android TV에서 폴백이 작동하지 않습니다.
폴백이 활성화되고 VMAP 응답에 빈 광고 중단이 있는 경우 재생이 중단되는 추가 문제가 해결되었습니다.

**버전 1.4.14 (1412)**

* Zendesk #17245 - Android TV에서 폴백이 작동하지 않습니다.
대체 광고에 대한 크리에이티브 재패키징을 비활성화하기 위한 제한을 제거했습니다.

**버전 1.4.13 (1388)**

* Zendesk #3502 - 광고 중단 중 HLS 클라이언트 기반 페일오버 지원
광고 중단 기간 동안 라이브 프로필 오류가 발생할 때 기본 매니페스트에 대한 장애 조치(failover)를 허용합니다.

* Zendesk #3875 - 재생 중 탭 충돌
HttpUrlConnection과 cURLm 간의 충돌을 해결하려면 타사 라이브러리를 사용하십시오.

* Zendesk #4450 - 컨텐츠 해결 프로그램의 단일 배치에 대한 사용자 지정 메타 데이터를 설정하는 문제
기회 설정에 setter를 추가합니다.

**버전 1.4.12 (1388)**

* Zendesk #2751 - CSAI 및 CRS | 향상:특정 미디어 파일 URL에서 동적 요소를 처리합니다.
동적 크리에이티브 URL을 사용하여 광고를 적절히 처리하도록 Creative Repackaging Service를 업데이트했습니다.

* Zendesk #3965 - 트릭플레이에서 일반적인 재생으로 다시 전환하면 재생을 시작하기 전에 잠시 앞으로 이동합니다.
   * Fix에는 GetStreamTime을 계산하는 대신 모든 변수가 업데이트될 때까지 비율이 변경되기 전 시간을 반환하는 TVSDK가 포함됩니다.
   * 스트림 끝 근처에 트릭 플레이 속도를 변경할 때 발생하는 충돌 문제가 수정되었습니다.
   * 트릭 플레이 중에 현재 시간 계산을 수정했습니다.

* Zendesk #3978 - 8x와 16x가 자주 멈추는 상태에서 트릭을 재생합니다.
   * 버퍼링을 지속하지 않도록 항상 가장 낮은 비트 전송률을 사용하여 트릭 재생 프로필을 선택합니다.
   * 높은 트릭 재생 속도를 위해 건너뛰기 프레임 간격을 늘립니다.
   * 트릭 재생 중에 버퍼의 대상 길이에 도달한 후 버퍼가 계속 증가하는 문제를 해결합니다.

* Zendesk #3992 - 추가 트릭플레이 속도.
TrickPlay는 16배 이상 높은 요금을 적용하도록 업데이트되었습니다.+/- 32, +/-64 및 +/-128도 이제 허용됩니다.

* Zendesk #4007 - GEOB 개체를 타임라인 메타데이터의 일부로 해석(Android 및 웹).
setByteArray 및 getByteArray API가 추가되었습니다.

* PTPLAY-7301 - 임의 액세스 포인트에서 즉시 시작
0이 아닌 시작점을 허용하도록 Instant On이 업데이트되었습니다.

**버전 1.4.11 (1363)**

* Zendesk #2076 - Android 4.0.3의 Motorola Xoom에서 비디오를 재생할 때 자주 끊김
허용 목록에 장치를 추가하여 프로필이 높은 콘텐츠를 재생하려고 하지 않도록 합니다.

* Zendesk #2197 - `[Ads]` 광고 오류 추적
경고 알림과 함께 OperationFailedEvent를 전달합니다.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 매크로가 채워지지 않음
   * 인라인 광고 크리에이티브가 불량한 경우 오류 코드 400이 표시됩니다.
   * `[ERRORCODE]` 매크로가 URL 인코딩됩니다.

**버전 1.4.10 (1354)**

* Zendesk #2941 - 라이브 에셋에 검색 가능한 범위에 &quot;0&quot;이 없습니다.
이전에는 라이브 스트림의 시작을 검색할 때 3개의 세그먼트 버퍼가 있었는데 이제 실시간 스트림의 맨 처음 시작(즉, 첫 번째 세그먼트의 시작)으로 이동할 수 있습니다.

* Zendesk #3169 - Update reference player with Adobe Analytics integration참조 플레이어가 Adobe Analytics 라이브러리로 업데이트되어 가져오기 예가 되었습니다.
* Zendesk #3299 - 설명 재생 동작 설명
   * 트릭 재생을 중지한 후 재생 상태로 돌아가는 데 몇 초(때로 25초 이상)이 걸릴 수 있는 버그를 수정했습니다.
   * 동일한 미디어에서 두 번째 트릭 재생을 호출하면 현재 시간에 스트림이 정지되는 버그가 수정되었습니다.
* Zendesk #3433 - Android 및 Flash - 자막 문제

WebVTT용 GetLine이 패킷에 대해 조정된 길이 &lt;CR>&lt;LF>를 준수하지 않았습니다.마지막 캡션은 이전 캡션의 문자를 포함할 수 있습니다.

* PTPLAY-6243 - 참조 플레이어를 강화하여 디버그 정보 캡처

Android 샘플 참조 플레이어는 디버그 로그를 켜고 결과를 이메일로 보내는 옵션과 함께 향상되었습니다. 이 옵션은 참조 플레이어의 로그 메뉴 아래에 있습니다.

**버전 1.4.9 (1332)**

* Zendesk #2649 - 초기 버퍼가 꽉 찼기 전에 버퍼 완료 발생

비디오 발표자를 재생할 준비가 되기 전에 비디오 엔진이 상태를 PLAYING으로 설정하는 경우가 있습니다. 찾기 전에 버퍼 상태가 높을 때 발생합니다. 비디오 엔진에 낮은 버퍼 상태를 알려 문제를 수정했습니다. 비디오 엔진의 버퍼 상태가 낮으면 [재생]을 호출하면 상태가 PLAYING 대신 BUFFERING으로 변경됩니다. 상태가 PLAYING으로 변경되면 재생이 다시 시작됩니다.

* Zendesk #2846 - 개선 요청:Auditude 라이브러리에서 수행하는 호출에 대해 서로 다른 사용자-에이전트 문자열을 설정하는 기능을 제공합니다.

광고 관련 호출인 auditudeSettings.setUserAgent(&quot;user/agent&quot;)를 위한 사용자 에이전트를 설정하기 위해 새 API가 추가되었습니다. 설정된 사용자 에이전트가 없으면 기본값이 사용됩니다. 이는 광고 관련 호출을 위한 사용자 에이전트에만 영향을 미치며, 미디어 호출을 위한 사용자 에이전트는 &quot;Adobe Primetime&quot;+&lt;기본 사용자 에이전트>가 변경되지 않습니다.

**버전 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 로컬 오류 ...파편화된 HTTPStreamer::ThreadParseManifest()에서 매니페스트를 로드하지 못하는 경우 URL 도메인이 localhost인지 확인하고, 그렇다면 도메인을 127.0.0.1으로 변경하고 ThreadParseManifest를 다시 호출하십시오.
* Zendesk #3072 - 낮은 비트 전송률로 자동 전환 0 PTS 페이로드를 건너뛰도록 버퍼 길이 계산을 변경했습니다.
* Zendesk #3168 - WebVTT 자막은 처음 10초 동안만 표시됩니다.
* Zendesk #3193 - TVSDK의 프로필 변경 API 요청, PlaybackEventListener.onProfileChanged()가 추가되었습니다.

**버전 1.4.7 (1311)**

* Zendesk #2197 - 광고 오류 추적. 매니페스트를 로드하지 못하는 자산에 대한 알림을 추가했습니다.
* Zendesk #2575 - PSDK는 비디오 전에 MARK 사용자 정의 스트리밍 광고를 무시합니다.
* Zendesk #2719 - Win Death with auditude 광고, auditude 플러그인의 상대 url로 리디렉션될 때의 고정 비콘 추적
* Zendesk #2760 - TrickPlay 모드 중에 DISCONTINUITY 태그가 무시됩니다.
* Zendesk #2805 - 재생 시작 시 플레이어 충돌, Zendesk와 동일한 수정 #2719
* Zendesk #2817 - Android 플레이어 - 2.0초에서 3.0초로 디코딩 버퍼를 확장하여 플레이어에서 가끔 정지 및 재생을 중지합니다.
* Zendesk #2839 - Adobe Primetime SDK가 ARMv8 칩셋을 지원합니까? Galaxy S6에서 발견된 충돌 문제에 대한 수정 사항이 추가되었습니다.
* Zendesk #2885 - Auditude 충돌 재생, Zendesk와 동일한 수정 #2719
* Zendesk #2895 - 10분 재생 후 라이브 HLS 오류가 일관되게 발생함
* Zendesk #2925 - Android 개발 빌드(1.4.5)에 대한 피드백이 입력 대기열에 추가되면 PTS가 음수인 경우 디코더는 항상 미래 패킷에 대한 음수 출력 PTS를 가져오는 이상한 상태로 전환됩니다. 이 문제를 방지하기 위해 음수이면 입력 PTS가 0으로 설정됩니다.
* PTPLAY-4645 - openssl에서 RC4 암호 지원을 해제합니다. RC4에 대한 알려진 악용이 있다. 즉, RC4만 지원하는 서버와 연결을 시도하면 연결이 실패합니다.

**버전 1.4.6 (1282)**

* Zendesk #2192 - 빠른 스위치 구현을 제거하여 네트워크 상태가 좋지 않은 경우에도 비트 전송률이 항상 낮은 것은 아닙니다.
* Zendesk #2631 - Android에서 아랍어 자막:아랍어 글꼴의 글꼴 크기를 조정하여 여러 줄의 텍스트가 잘려 보입니다.
* Zendesk #2844 - 노트 4 및 조각 다운로드 시간의 버퍼링이 정확하지 않습니다.

이 문제는 비디오 세그먼트 다운로드 간 지연을 대역폭 계산에 추가하고 다운로드 시간 계산 로직이 전체 요청 주기 시간을 사용하도록 하여 해결되었습니다.

* Zendesk #2908 - 아랍어 스크립트용 대체 글꼴 2개를 추가하여 Nexust 5, 6 및 7에서 작동하지 않는 아랍어 자막이 수정되었습니다.
* PTPLAY-4627 - Nielson appsdk를 버전 1.2.3.7으로 업데이트
* PTPLAY-5084 - 라이브 매니페스트 업데이트 기본 페일오버 지원

**버전 1.4.5 (1248)**

* Zendesk #1757 - 일부 비디오 비트 전송률 프로필, Nexus 4 및 Nexus 7 충돌 문제가 수정되었습니다.
* Zendesk #2072 - AdEvent에 대한 TimedMetadata에 전체 URL이 &quot;http&quot;만 포함되어 있지 않습니다.
* Zendesk #2192 - 비트 전송률이 항상 낮은 것은 아닙니다.
* Zendesk #2256 - Access to Playlist, updated 기본 PSDK to dispatch on the master playlist.
* Zendesk #2269 - WebVTT를 사용하여 화면에 동시에 두 개의 자막 언어가 표시됩니다.
* Zendesk #2417 - 플레이어에서 재생 시작 전에 자막을 다운로드하려고 하면 WebVTT가 세그먼트 번호 일치에 잘못된 세그먼트 번호 변수를 사용하고 있었습니다. 세그먼트 색인이 0부터 시작되는 미디어에만 버그가 표시됩니다.
* 일시 중단 후 비트 전송률 변경이 발생하는 경우 Zendesk #2470 - PSDK가 일시 중단 상태에서 반환되지 않습니다. 스마트 검색이 RestoreGPUResource(일시 중단 상태의 복원 플레이어)에 의해 호출되고 그 전에 스트림 스위치가 감지되면 스마트 검색이 완료되지 않고 지속적인 버퍼링으로 이어집니다.
* Zendesk #2451 - 닫힌 캡션 &#39;아래쪽 인세트&#39;, 캡션 코드에 &#39;bottomInset&#39; 매개 변수를 추가했습니다.
* Zendesk #2480 - HTTP 302 리디렉션 최적화 비활성화, useRedirectedUrl 속성 설정 지원 추가
* Zendesk #2486 - 타사 비콘
* Zendesk #2547 - 아랍어 자막:텍스트를 오른쪽으로 정렬해야 합니다.

**버전 1.4.4 (1195)**

* Zendesk #1158 - Huawei Valiant에서 재생 실패(Y301A1)
* Zendesk #1709 - 잘못된 미디어 크기 및 비디오
* Zendesk #1757 - 동일한 스파/pps 데이터가 있는 스트림 간 프로필 전환 후 재생되는 오디오만
* Zendesk #2095 - HTTP 307 상태(리디렉션)를 사용하면 Adobe 플레이어에서 재생을 중단할 수 있습니다.
* Zendesk #2126 - 마지막 ADEVENT에 대한 TimedMetaData 이벤트 누락, 마지막 세그먼트 이후에 존재하는 구독 태그가 AVE의 PSDK에 보고되지 않았습니다.
* Zendesk #2227 - Lockup in VideoEngine nativeReset 및 nativePause
* 버그 #3921755 - OpenSSL 라이브러리 업데이트 버전 1.0.1L

**버전 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - 닫힌 캡션 켜기 및 끄기
* PTPLAY-1818 - 되감기 트림 재생이 광고를 지나치지 않고 광고에서 정지합니다.
* PTPLAY-2736 - WebVTT 캡션이 포함된 스트림의 재생이 완료되면 이전에 표시된 WebVTT 캡션이 화면에 표시됩니다.
* PTPLAY-3773 - 광고 위치 후에 스트림 재생이 시작될 때 중간 롤 광고가 재생되지 않습니다.

**버전 1.4.2**

* Zendesk #1561 - Primetime의 HLS 클라이언트 기반 장애 복구 지원 프로그램 날짜 시간을 사용하여 장애 조치를 해결합니다.
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0입니다(오디오 전용으로 고정되지 않음).
* Zendesk #1626 - Player의 잠재적 메모리 누수. 실제 메모리 누수가 아니라, NotificationHistory가 지난 1000개의 알림을 저장하는 동안 문제가 발생하여 100개로 줄었습니다.
* Zendesk #2192 - 비트 전송률이 항상 낮은 것은 아닙니다.

**버전 1.4.1 (1121)**

* Zendesk #1951 - 4.0.x 장치에서 VideoEngine.nativeReset()을 잠금
* Zendesk #2064 - 특정 Intel 기반 Android 장치의 기본 충돌 SIGSEGV
* Zendesk #2075 - Lockup in VideoEngine.nativeReleaseGPUResource on 4.0.x 장치
참고:이 빌드는 Android 5.0(Lollipop)을 지원하기 위해 ***required***입니다.
* Zendesk #1513 - Android Lollipop 지원
* Zendesk #1709 - 잘못된 미디어 크기 및 비디오
* Zendesk #1871 - WebVTT 캡션이 가끔 사라지고 실시간 스트림을 WebVTT 캡션으로 볼 때 다시 나타날 수 있습니다.
* Zendesk #1996 - PSDK에 타임라인 마커가 표시되지 않음 1.4.0
* Zendesk #2046 - PSDK 1.4.1.1113 충돌, Auditude에서 반환된 광고가 없을 때 실시간 스트림의 충돌 문제 수정
* 버그 #3769657 - curl 버전을 7.38.0 버전으로 업데이트
* PTPLAY-1575 - ABR 재생이 오디오 전용 스트림으로 시작한 다음 오디오/비디오 스트림으로 전환하면 오디오가 계속 진행되는 동안 비디오가 렌더링되지 않습니다.
* PTPLAY-2499 - 최신 취약점을 해결하기 위한 1.0.1j 버전 OpenSSL로 업데이트
* PTPLAY-2632 - Android Lollipop에서 mid 롤 광고 완료 후 비디오가 복구되지 않음
* PTPLAY-2678 - Android Lollipop에서 실시간 수명 테스트 동안 비디오 가판대

**버전 1.4.0**

* Zendesk #1024 - 매니페스트를 통해 스트림에서 광고를 제거하는 기능
* Zendesk #1293 - 닫힌 캡션 트랙 선택 문제.
* Zendesk #1590 - LoadInfo.MediaDuration은 항상 0이고 mediaDuration은 이제 올바른 값을 표시합니다.
* Zendesk #1629 - Galaxy S4에서 광고 재생 종료 시 플레이어/앱 충돌
* 0x03 ETX 코드가 없을 때 Zendesk #1674 - ClosedCaption이 표시되지 않음, 708 캡션 표시를 교정합니다.
* PTPLAY-2157 - 스트림에서 시각적으로 다른 스타일을 설정하고 확인한 후에도 기본 닫힌 캡션 스타일이 getter에 의해 반환되었습니다. 이제 닫힌 캡션 스타일 속성에 설정된 값이 표시됩니다.

## 1.4 {#known-issues-in}의 알려진 문제

**버전 1.4.31**

* PTPLAY-16803 - 캡션 시스템이 작동하기 위해 비디오가 필요하므로 닫힌 캡션은 오디오 전용 컨텐츠에서 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* PTPLAY-1634 - 동일한 구독 태그의 라이브 윈도우에 다른 타임스탬프가 있습니다. 라이브 윈도우를 이동할 때 해당 윈도우에 있는 동일한 태그의 타임스탬프가 같아야 합니다. 하지만 같은 태그도 타임스탬프가 다른 경우가 있습니다.
* PTPLAY-3197 - 연속 재생 1 시간 이후 Acer Iconia 디바이스에서 신호 11 SIGSEGV 오류가 발생하는 충돌
* PTPLAY-3310 - 비트 전송률이 낮은 오디오를 사용하면 Acer Iconia에서 오디오가 끊김/끊김 현상이 발생합니다.
* PTPLAY-3355 - 연속 재생 시간 ~ 1시간 후 4.0.x의 Motorola Xoom에서 WIN DEATH 충돌
* PTPLAY-3557 - 광고 중단에서 되감으로써 스트림이 완료됩니다.
* PTPLAY-7079 - Android 클라이언트의 재생 창이 보안 중지/하드 정지에서 작동하지 않습니다.
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 바뀌거나 Pulse로 나타날 수 있습니다. 자세히 살펴보는 것만
* #3761170 - SeekToLocal in Ads with Live에서는 광고 컨텐츠를 다시 검색할 수 없으므로 실시간 스트림용 currentTime API를 사용하는 것이 가장 좋습니다
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 할 때 두 개의 광고 마커가 함께 표시되는 경우가 있습니다. 이러한 광고 마커는 동일한 광고를 나타내고 한 개만 재생됩니다
* 버그 #3763373 - VOD 스트림에서 과거 광고를 검색할 때 광고 마커가 잠시 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 부작용은 없습니다
* 일부 장치에서는 알려진 재생 문제가 있습니다. [1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)의 알려진 장치 문제를 참조하십시오.
* 참조 구현 - 트릭 플레이는 샘플 응용 프로그램에서 구현되지 않습니다.
* 일부 Android TV 장치에서는 다음 전환 지점의 디코더 재설정으로 인해 검정 프레임을 볼 수 있습니다.
   * 트릭플레이 모드로
   * 늦게 바인딩 오디오 트랙 간 전환
   * 광고에서 기본 컨텐츠로.

**버전 1.4.23**

* 캡션 시스템에 비디오가 필요하므로 닫힌 캡션은 오디오 전용 콘텐츠에서 작동하지 않습니다. 비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.
* 버전 1.4.23부터 TVSDK는 Gingerbread OS 2.3을 지원하지 않습니다. 이는 TVSDK가 Gingerbread OS를 사용하는 장치에 대한 하드웨어 정보를 수집하기 위해 다음의 개인 Android 라이브러리를 사용하기 때문입니다.

   * `libstagefright.so`
   * `libcutils.so`

Android N 릴리스에서 Google은 이러한 비공개 라이브러리에 대한 액세스를 제거했습니다. Gingerbread OS는 현재 전세계 Android OS 시장의 1% 미만을 차지하기 때문에, 버전 1.4.23 이후, Gingerbread OS는 더 이상 TVSDK에서 지원되지 않을 것입니다.
버전 1.4.23(Android N 지원 포함) 이상을 사용하는 경우:
* minSdkVersion 버전 11을 사용하도록 앱을 업데이트하십시오.
* 최종 사용자가 OS 2.3을 실행하는 경우 SDK 버전은 애플리케이션의 minSdkVersion보다 작습니다. 시스템이 응용 프로그램의 설치 또는 업그레이드를 중단합니다.
* 최종 사용자가 OS 2.3보다 높은 버전을 실행하는 경우 애플리케이션이 올바르게 설치됩니다.

minSdkVersion을 업데이트하는 경우:

* 최종 사용자가 OS 2.3을 실행하는 경우 응용 프로그램이 설치되지만 재생은 작동하지 않습니다.
이는 업데이트 및 새로 설치할 때 적용됩니다.
* 최종 사용자가 OS 2.3보다 높은 시스템을 실행 중인 경우 앱이 올바르게 설치되고 내용이 올바르게 재생됩니다.

**버전 1.4.22**

* 스플라이스 아웃 및 스플리인 태그가 서로 너무 가까이 있는 경우, 광고의 조기 종료는 일부 미드롤 광고에서 작동하지 않습니다.

**버전 1.4.2**

* 광고 브레이크에서 되감으면 스트림이 완료됩니다.

Media Player가 광고 경계에 도달하면 트릭 플레이 되감기 작업 중에 MediaPlayer Player PlayerState.Complete를 잘못 전송합니다. 트릭 재생 모드에서 이 이벤트를 플레이어가 무시해야 하며 그렇지 않으면 SDK에서 상태를 올바르게 처리합니다.

**버전 1.4.0 (1086)**

* PTPLAY-1634 - 동일한 구독 태그의 라이브 윈도우에 다른 타임스탬프가 있습니다. 라이브 윈도우를 이동할 때 각 윈도우에 있는 동일한 태그의 타임스탬프가 같아야 합니다. 하지만 같은 태그도 타임스탬프가 다른 경우가 있습니다.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE가 가끔씩 일시 중단에서 대체 스트림으로/전환된 후 표시됩니다.
* 버그 #3726865 - MultiBitrate LBA 스트림이 오디오 전용 스트림에서 시작하는 경우 오디오/비디오 스트림으로 전환하면 비디오가 표시되지 않습니다. 오디오/비디오 스트림에서 시작해도 이 문제가 표시되지 않으며 오디오 및 오디오/비디오 스트림 간을 성공적으로 전환할 수 있습니다.
* 버그 #3760144 - Kindle Fire 7 및 Samsung Galaxy Nexus와 같은 일부 장치에서 스트림이 일시 중지되면 해상도가 바뀌거나 Pulse로 나타날 수 있습니다. 자세히 살펴보는 것만
* #3761170 - seekToLocal in Ads with Ads는 광고 콘텐츠로 다시 검색할 수 없습니다.라이브 스트림에 현재 시간 API를 사용하는 것이 가장 좋습니다.
* 버그 #3763370 - 광고가 있는 라이브 스트림에는 광고 마커가 하나만 있어야 할 때 두 개의 광고 마커가 함께 표시되는 경우가 있습니다. 이러한 광고 마커는 동일한 광고를 나타내고 한 개만 재생됩니다
* 버그 #3763373 - VOD 스트림에서 과거 광고를 검색할 때 광고 마커가 잠시 사라질 수 있습니다. 광고 마커가 복원되고 타임라인에 다른 부작용은 없습니다
* 일부 장치에서는 알려진 재생 문제가 있습니다. 자세한 내용은 [1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)의 알려진 장치 문제를 참조하십시오.
* 참조 구현 - 트릭 플레이는 샘플 응용 프로그램에서 구현되지 않습니다.

## 1.4 {#known-device-issues-in}의 알려진 장치 문제

| 장치 | 칩셋 | 문제 | 원인 | 해결 방법 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR 지연은 디코더를 다시 시작하므로 필요합니다. |  |  |
| HTC Desire(HTC Desire HD와는 다름) | QSD8250 | 비디오를 재생할 수 없습니다. VIDEO_PROFILE_NOT_SUPPORTED 오류를 반환합니다. | 욕망은 적절한 HW 디코더를 제공하지 않습니다. Stageright의 SW 디코더를 제공합니다. | 장치를 다시 시작합니다. |
| HTC EVO 4G | QSD8650 | HW 디코더가 없습니다. | Qualcomm에는 HW 디코더가 없습니다. | Android 4.x로 업그레이드 |
| Kindle FireSystem 버전 6.0 | TI OMAP4 | HLS 스트림을 재생하지 않습니다. AIR에서 비디오가 작동하지 않습니다. |  | 시스템 버전 6.3으로 업그레이드 |
| Kindle Fire HD | TI OMAP4 | 비디오를 재생할 수 없는 상태로 전환할 수 있습니다. VIDEO_PROFILE_NOT_SUPPORTED 및 UNRECOVERABLE_ERROR 오류를 반환합니다. | HW 디코더는 충돌 발생 후 HW 디코더를 완전히 종료하지 않으면 복구할 수 없는 상태로 전환됩니다. 장치의 기본 앱에서도 발생합니다. | 장치를 다시 시작합니다. |
| Kindle Fire HD 8.9 | Snapdragon 800 | 여러 ABR 스위치 후에 AVE 충돌이 발생합니다. |  |  |
| Motorola Atrix | Tegra2 | AIR 대신 AVE와 관련된 전반적인 성능 문제 오디오/비디오가 동기화되지 않고 비디오 재생이 9분에서 15분 간 재생된 후에 중지됩니다. 충돌. | AIR에서 실행하는 openGLES와 관련되었을 수 있습니다. 조사 중입니다. |  |
| Nexus 7(2세대) | S4Pro APQ8064 (Qualcomm) | 동영상을 30분 이상 일시 정지하면 장치가 정지됩니다. | Google에 보고된 장치 문제. | 앱이 긴 일시 정지 상태를 허용하지 않도록 시간을 초과해야 합니다. |
| Nexus S(GB) | 허밍 새 | HW 디코더를 사용하여 비디오를 재생할 수 없습니다. | Nexus S에는 Stageright 기반 HW 디코더가 없으므로 Android 2.3에서는 SW 디코더를 사용하고 있습니다. | ICS로 업그레이드 |
| Nexus S(ICS) | 허밍 새 | 비디오가 깜박이는 경우도 있습니다. | 데이터가 잘못되면 디코더가 잘못된 상태로 전환될 수 있습니다. | 장치를 다시 시작합니다. |
| Nook tabletAndroid OS:2.3 | TI OMAP 4 | 비디오가 재생되지 않고 앱이 정지됩니다. | Stagefright는 몇 번 앱을 실행한 후 불안정한 상태로 전환됩니다. mediaplayer::QueryCodecs 내어쓰기를 호출합니다. | 상태를 재설정하려면 장치를 다시 시작합니다. |
| 삼성 갤럭시 ACE | Qualcomm MSM7227 | SampleMediaPlayer 앱을 설치할 수 없습니다. | 더 일반적인 ARM v7 칩셋 대신 ARM v6을 사용합니다. FP/AIR는 이 장치를 지원하지 않습니다. |  |
| Samsung Galaxy ACE2Android OS:2.3.6 | 노바토르 U8500 | 비디오를 재생할 수 없습니다. | 이 칩셋은 AVE의 Android 사전 ICS에 대한 알 수 없는 디코더입니다. |  |
| Samsung Galaxy S2(GT-I9100) | Exynos | 비디오 성능이 이 장치에 적합한 것은 아닙니다. | HW 디코더가 잘못된 PTS로 디코딩된 프레임을 반환합니다. 디코더가 프레젠테이션 시간 대신 디코딩 시간을 사용하는 것 같습니다. |  |
| Samsung Galaxy S2 Android OS:2.3.6 | TI OMAP4 | 비디오를 시작할 때 충돌합니다. |  | Android 2.3.7 또는 4.x로 업그레이드 |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | 간헐적으로 비디오가 정지되고 오디오만 재생되면 응답이 없습니다. |  |  |
| 삼성 갤럭시 S3 I747M | SAMSUNG_M2ATT | 비디오가 중지됩니다. | 조사 중입니다. |  |
| 삼성 Galaxy Tab 1 v10.1 | Tegra 2 | MBR 전환에는 최대 3초가 걸릴 수 있습니다. | MBR 충돌에 대한 수정 사항으로 모든 스트림 스위치에 대한 디코더를 다시 시작합니다. 이 디코더는 최대 3초까지 걸릴 수 있습니다. |  |
| 삼성 갤럭시 Y |  | SampleMediaPlayer 앱을 설치할 수 없습니다. | 더 일반적인 ARM v7 칩셋 대신 ARM v6을 사용합니다. FP/AIR는 이 장치를 지원하지 않습니다. |  |
| Xoom | 테그라 | 전환하는 데 사용할 프레임이 몇 개 없습니다. 디코더를 다시 시작하지 않습니다. | OMXAL 제한. |  |

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 설명서를 참조하십시오.
