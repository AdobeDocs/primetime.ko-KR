---
title: Android용 TVSDK 2.4.1 릴리스 노트
seo-title: Android용 TVSDK 2.4.1 릴리스 노트
description: Android용 TVSDK 2.4.1 릴리스 정보에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.
seo-description: Android용 TVSDK 2.4.1 릴리스 정보에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 0%

---


# Android용 TVSDK 2.4.1 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 2.4.1 릴리스 정보에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe은 Android용 TVSDK 2.4.1을 출시했습니다.

이 버전의 TVSDK를 사용하려면 시스템이 [시스템 요구 사항](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)에 설명된 요구 사항을 충족하는지 확인하십시오.

다음은 설명서를 찾을 수 있는 곳입니다.

・ Android용 온라인 도움말 시스템 TVSDK 2.4 도움말

・ Android Java API용 [Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs는 TVSDK 소스 코드에서 직접 자동으로 생성되므로 완벽한 권위자입니다.

・ Android C++ API용 [C++ API 설명서 TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

각 Java 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 Javadocs보다 더 많은 설명서가 포함되어 있으므로 Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.

・ 마이그레이션 안내서([TVSDK 2.4 for Android 마이그레이션 안내서](../migration-guides/tvsdk-14-25-android.md))

이 안내서에서는 TVSDK 1.4를 기반으로 한 애플리케이션을 TVSDK 2.4를 기반으로 한 애플리케이션으로 마이그레이션하기 위해 수정해야 하는 사항을 설명합니다.

## 새 기능 {#new-features}

Android용 TVSDK 2.4.1은 이전 버전보다 향상된 많은 성능을 제공합니다. 고품질의 시청 환경을 제공합니다.

이 버전에는 버전 2.4 및 2.4.1의 모든 기능이 포함되어 있으며, 더 이상 사용되지 않습니다.

버전 2.4.1의 새로운 주요 기능은 다음과 같습니다.

* HLS 버전 4 기능

   * **실시간, 리니어 및 VOD 스트림을 위한 플레이어 컨트롤을 사용하여 비디오 재생** (재생, 일시 정지, 검색)을 할 수 있습니다.
   * **자막.** TVSDK는 608/708 자막을 표시하고 글꼴, 글꼴 크기, 색상 및 배경을 선택할 수 있습니다. 또한 롤업 캡션이 포함된 비디오를 지원하고 사용 가능한 경우 언어 트랙 간을 전환할 수 있습니다.
   * **Trick play** modes는 신속하게 가져오고 I-Frames를 사용하는 HLS 스트림의 경우 되감기를 할 수 있습니다. 모든 비디오 재생 컨트롤은 컨텐츠에서 작동합니다. 속도가 0에서 1인 외부 비디오 재생 모드에서 슬로우 모션(앞으로)을 사용할 수 있습니다.
   * **ABR(적응형 비트 전송률)** 을 사용하면 네트워크 및 기타 조건에 따라 동일한 컨텐츠 스트림의 여러 버전을 동적으로 선택하여 재생할 수 있습니다. 매개 변수를 동적으로 또는 매니페스트 파일에서 설정하여 공격적이고, 중재적이며, 보수적인 선택 정책 중에서 선택할 수 있습니다.
   * **바이트** 범위단일 TS 파일에 여러 TS 세그먼트를 포함할 수 있도록 설정합니다.
   * **다른 오디오** 변환플레이어에서 사용 가능한 오디오 트랙 간을 전환할 수 있도록 합니다.
   * **ID3 지원.** TVSDK는 ID3 오디오 메타데이터가 포함된 HLS 오디오 및 비디오 스트림(예: 아티스트 이름, 제목 및 앨범)을 재생할 수 있습니다.
   * **장애 조치(failover). **TVSDK는 호스트 서버, 재생 목록 파일 및 세그먼트에 장애가 발생하더라도 중단 없이 계속 재생할 수 있는 전략을 사용합니다.
   * **멀티채널 오디오 통과(DD+).** TVSDK는 Dolby Digital Plus 오디오(E-AC3) 데이터를 지원 하드웨어에 전달할 수 있습니다.

* 컨텐츠 보호 기능

   * **HLS용 DRM.** 모든 비디오 재생 API는 Adobe 액세스로 보호되는 암호화된 비디오 컨텐츠와 연동됩니다. 다음 DRM 기능이 지원됩니다.

      * 라이선스 순환
      * 키 회전
      * 라이선스 캐싱
      * 정책 시간
      * IV 회전

* **AES 128 재생.** TVSDK는 키 크기가 128비트인 고급 암호화 표준(AES) HLS 컨텐츠를 재생할 수 있습니다.
* **보호된 HLS(PHLS)** 는 실시간 및 VOD 스트림에 대해 HLS에 대한 경량 DRM을 활성화하는 Adobe 액세스 기능의 하위 집합인 미리 만들어진 DRM 정책의 제한된 세트를 제공합니다.

* 광고/대체 컨텐츠 및 상용화 기능

   * **서버측 삽입된 광고에 대한 추적.** TVSDK는 Adobe 클라우드 광고 삽입 서비스에서 삽입한 광고를 추적할 수 있습니다. VOD 및 라이브/리니어 스트림을 위해 VAST2, VAST3 및 VMAP 포맷의 선형 광고를 지원합니다.
   * **사용자 지정 HLS 태그입니다.** TVSDK는  `MediaPlayerConfig` 클래스를 사용하여 스트림에 사용자 지정 HLS 태그가 나타날 때 플레이어 응용 프로그램에 알림을 활성화합니다.
   * **클라이언트측 광고 삽입.** Auditude 광고 삽입 라이브러리는 Adobe Auditude 서버와 연동하여 프리롤, 미드롤 또는 포스트롤 위치에서 라이브, 선형 및 VOD 컨텐츠에 동적으로 삽입하는 광고를 해결합니다.
   * **맞춤형 광고 해상도** 이  `ContentResolver, OpportunityGenerator,` 및  `MediaPlayerClientFactory` 인터페이스를 통해 사용자 지정 광고/대체 컨텐츠 확인자를 구현하고 TVSDK와 연동되도록 사용자 지정 기회 탐지기를 등록할 수 있습니다. `TestAdResolver` 및 `AuditudeResolver` 클래스는 컨텐츠 해결 프로그램 구현의 C++ 예를 제공합니다. `samples/jspsdk/testapp/psdk.js`에서 Javascript 예를 찾을 수 있습니다.
   * **일관된 광고 행동** 이  `AdPolicySelector` 인터페이스를 사용하여 컨텐트에 광고가 있을 때 검색 및 트릭 플레이와 같은 작업을 수행할 때 모든 플레이어에서 일관된 동작을 구현할 수 있습니다. 직접 구현하지 않는 경우 TVSDK는 `DefaultAdPolicySelector`을 사용합니다.
   * **C3 광고 제거/바꾸기** 적절한 TVSDK API를 사용하여 맞춤형 컨텐츠 범위를 제거하고 추가 준비 작업 없이 새로운 광고를 동적으로 삽입할 수 있습니다. 이 기능은 라이브/선형 컨텐츠가 브로드캐스트된 다음 정리하지 않고 즉시 On-Demand로 제공되었을 때 유용합니다.

다음은 주요 새로운 기능 버전 2.4입니다.

* **VOD 및** 라이브TV에 대한 즉각적인 설정TVSDK는 재생을 시작하기 전에 미디어를 초기화하며 버퍼링합니다. 백그라운드에서 여러 `MediaPlayerItemLoader` 인스턴스를 동시에 실행할 수 있으므로 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 재생이 즉시 시작됩니다. 또한 TVSDK 2.4는 실시간 스트림을 위한 Instant On을 지원합니다. 라이브 창이 이동하면 라이브 스트림이 다시 버퍼링됩니다.

* **성능 개선 **새로운 TVSDK 2.4 아키텍처는 다음과 같은 다양한 성능 향상을 제공합니다.

   * **하위 세분화**  - TVSDK는 각 조각 크기를 줄여 재생을 가능한 한 빨리 시작합니다.
   * **병렬 광고 다운로드**  - TVSDK는 광고를 중단하기 전에 컨텐츠 재생과 동시에 광고를 프리페치하므로 광고와 컨텐츠를 매끄럽게 재생할 수 있습니다.
   * **레이지 광고 해상도**  - 이 기능을 사용하면 재생을 시작하기 전에 프리롤 광고가 아닌 광고의 해상도를 기다리지 않아도 되므로 시작 시간이 줄어듭니다. 검색 및 트릭 플레이와 같은 API는 모든 광고가 해결될 때까지 허용되지 않습니다.

* **MP4 컨텐츠 재생**

이 버전의 TVSDK는 MP4를 기본 컨텐츠로 재생하는 것을 지원합니다.

* **영구 네트워크 연결**

TVSDK는 재사용 가능한 네트워크 연결 세트를 유지 관리하므로 각 네트워크 요청에 대해 네트워크 연결을 만들고 손상하는 간접비를 발생시키지 않습니다.

* **해상도 기반의 출력 보호**

이 기능은 재생 제한 사항을 특정 해상도에 연결하여 보다 세밀하게 다듬은 DRM 컨트롤을 제공합니다.

* **적응형 비트 전송률(ABR)로 트릭 재생**

이 기능을 통해 TVSDK는 트릭 재생 모드에서 iFrame 스트림 간을 전환할 수 있습니다. iFrame이 아닌 프로파일을 사용하여 보다 빠른 속도로 트릭 재생을 수행할 수 있습니다.

* **매끄러운 트릭 플레이**

이러한 향상된 기능은 사용자 경험을 향상시켜 줍니다.

・ 트릭 재생 중 대역폭 및 버퍼 프로필을 기반으로 적응 비트 전송률과 프레임 속도를 선택할 수 있습니다.

・ IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps의 빠른 재생을 수행할 수 있습니다.

* **향상된 ABR 논리**

새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 속도 및 측정된 대역폭을 기반으로 합니다. 따라서 ABR은 대역폭이 변경될 때 올바른 비트 전송률을 선택하고 버퍼 길이가 변경되는 속도를 모니터링하여 비트율 스위치가 실제로 발생하는 횟수를 최적화합니다.

* **청구**

TVSDK는 고객 판매 계약을 준수하여 청구 목적에 필요한 주기적인 사용 보고서를 자동으로 수집합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림 기간에 따라 콘텐츠 유형, 광고 삽입 가능 플래그, drm 활성화 플래그 등의 청구 측정 지표를 Adobe Analytics Primetime 소유 보고서 세트로 전송합니다. 이 경우 고객의 자체 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하거나 포함시키지 않습니다. 요청 시 이 청구 사용량 보고서는 고객에게 정기적으로 전송됩니다. 청구 기능의 첫 번째 단계로서 사용 비용 청구 전용입니다. 설명서에 설명된 API를 사용하여 판매 계약에 따라 구성할 수 있습니다.

## 지원되는 기능 {#supported-features}

Android 2.4용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

>[!NOTE]
>
>아래 기능 매트릭스 표에서 이 기능은 현재 릴리스에서 지원됨을 √ 의미합니다.

### 코어 재생 기능 {#core-playback-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| 일반 재생(재생, 일시 정지, 검색) | VOD + 라이브 | √ | √(VOD만 해당) |
| FER - 일반 재생(재생, 일시 중지, 검색) | FER VOD | √ | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | √ | √ |
| 적응형 비트 전송률 전환 논리 | VOD + 라이브 | √ | 지원되지 않음 |
| 오디오 전용 재생 | VOD + 라이브 | √ | 지원되지 않음 |
| 자막 - 608/708 | VOD + 라이브 | √ | √(VOD만 해당) |
| 자막 - WebVTT | VOD + 라이브 | √ | √(VOD만 해당) |
| 매니페스트 장애 조치(Manifest Failover) | VOD + 라이브 | √ | √(VOD만 해당) |
| 고급 페일오버 | VOD + 라이브 | √ | √(VOD만 해당) |
| QoS 및 플레이어 알림 | VOD + 라이브 | √ | √(VOD만 해당) |
| 쿠키 헤더 지원 | VOD + 라이브 | √ | √(VOD만 해당) |
| 사용자 정의 헤더 지원 | VOD + 라이브 | 지원되지 않음 | 지원되지 않음 |
| 버퍼 컨트롤 매개 변수 설정 | VOD + 라이브 | √ | √(VOD만 해당) |
| 적응형 비트 전송률 컨트롤 설정 | VOD + 라이브 | √ | √(VOD만 해당) |
| HLS(사용자 지정 매니페스트 태그)/이벤트 스트림(DASH) | VOD + 라이브 | √ | √(VOD만 해당) |
| 늦게 바인딩된 오디오 | VOD + 라이브 | √ | √(VOD만 해당) |
| 302 리디렉션 | VOD + 라이브 | √ | √(VOD만 해당) |

### 고급 재생 기능 {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>기능</strong></td> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>대시</strong></td> 
  </tr>
  <tr>
   <td>오프셋을 사용한 재생</td> 
   <td>라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>오디오 전용 재생</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>트릭 플레이 </td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>부드러운 트릭 플레이(ABR 사용)</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>ID3 구문 분석(HLS)/DASH(Timed Metadata)</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>일시 중단 </td> 
   <td>VOD + 라이브</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>즉시 켜기</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>HLS(Dis연속성 마커 지원) </li> 
     <li>다기간(DASH)</li> 
    </ul> </td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>302 리디렉션 지속</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD만 해당)</td> 
  </tr>
  <tr>
   <td>축소판 스크러빙(Iframe 및 JPEG)</td> 
   <td>VOD + 라이브</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>스트림 무결성 </td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
 </tbody>
</table>

### 핵심 Ad Insertion 기능(CSAI) {#core-ad-insertion-features-csai}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| 일반 재생, 광고 사용 | VOD + 라이브 | √ | √(VOD 프리롤만) |
| 광고가 활성화된 FER 컨텐츠 | VOD | √ | 지원되지 않음 |
| 기본 광고 비헤이비어 | VOD + 라이브 | √ | √(VOD 프리롤만) |
| VAST 2.0/3.0 | VOD + 라이브 | √ | √(VOD 프리롤만) |
| VMAP 1.0 | VOD + 라이브 | √ | √(VOD 프리롤만) |
| MP4 광고 | VOD + 라이브 | √(CRS) | √(CRS에서 프리롤만) |

### 고급 Ad Insertion 기능(CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>기능</strong></td> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>대시</strong></td> 
  </tr>
  <tr>
   <td>광고를 사용하여 트릭 플레이</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>광고 전용 </td> 
   <td>VOD</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>타깃팅 매개 변수</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만)</td> 
  </tr>
  <tr>
   <td>사용자 지정 매개 변수</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 동작</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 태그</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 해상도</td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>자유로운 사용자 지정 광고 확인자</td> 
   <td>VOD</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>C3 광고 교체 </td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>레이지 광고 로딩</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>불연속성 마커 지원 - SSAI(HLS) </li> 
     <li>다기간(DASH)</li> 
    </ul> </td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>부록 광고, 배너 광고 및 클릭 가능한 광고</td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>√(VOD 프리롤만)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + 라이브</td> 
   <td>√(JS) </td> 
   <td>√(VOD 프리롤만)</td> 
  </tr>
  <tr>
   <td>조기 광고 종료</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>규칙 기반의 크리에이티브 VOD + 라이브 우선 순위</td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>CRS 규칙 </td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
 </tbody>
</table>

## 콘텐츠 보호 기능 {#content-protection-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| AES 암호화 | VOD + 라이브 | √ | √(VOD만 해당) |
| 샘플 AES 암호화 | VOD + 라이브 | √ |  |
| 토큰화된 스트림 | VOD + 라이브 | √ |  |
| DRM | VOD + 라이브 | Primetime DRM만 해당(향후:Widevine) | 와이어드만 |
| 외부 재생(RBOP) | VOD + 라이브 | Primetime DRM만 해당 | 지원되지 않음 |
| 라이선스 순환 | VOD + 라이브 | Primetime DRM만 해당 | 지원되지 않음 |
| 키 회전 | VOD + 라이브 | Primetime DRM만 해당 | 지원되지 않음 |

### 통합 기능 {#integration-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| Adobe Analytics VHL 통합 | VOD + 라이브 | √ | √ |
| 청구 | VOD + 라이브 | √ | 지원되지 않음 |

## 지원되지 않는 기능 {#features-not-supported}

이 버전의 TVSDK는 지원되지 않습니다.

* 광고 중단.
* 트릭 플레이의 느린 동작
* MP4 컨텐츠를 사용하여 원하는 대로 간편하게 제작
* MP4 기본 컨텐츠로 광고 삽입
* 광고 재생 시간을 검색합니다.
* 오디오 전용 미디어를 사용한 광고 재생

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 디바이스별(Samsung Galaxy Tab 4)에서 오디오가 장착된 VOD DRM LBA 충돌 및 광고 클릭
* 포스트롤 광고는 특정 컨텐츠에 대해 재생되지 않습니다.
* CJK 언어로 닫기 캡션을 설정할 수 없습니다.
* 비디오는 VOD와 라이브 사이에 자동으로 트릭 모드에서 나올 수 있습니다.
* VHL - 옵셋에서 컨텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 event:type:play 광고에 대한 VHL 하트비트 호출을 재생하면 광고가 없습니다.
* adBreakPolicy SKIP를 선택해도 프리롤 광고가 재생됩니다.
* 전체 상태 플레이어로 이동한 후 포스트롤 광고에 대해 SKIP adBreakPolicy가 있는 재생 상태로 돌아갑니다.

비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 문서를 참조하십시오.