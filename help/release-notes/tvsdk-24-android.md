---
title: Android용 TVSDK 2.4.1 릴리스 노트
description: Android용 TVSDK 2.4.1 릴리스 노트에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Android용 TVSDK 2.4.1 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 2.4.1 릴리스 노트에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe이 Android용 TVSDK 2.4.1을 출시하고 있습니다.

이 버전의 TVSDK를 사용하려면 시스템에서 다음에 설명된 요구 사항을 충족하는지 확인하십시오. [시스템 요구 사항](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

여기에서 설명서를 찾을 수 있습니다.

· Android 도움말용 온라인 도움말 시스템 TVSDK 2.4

· [Android Java API용 Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs는 TVSDK 소스 코드에서 직접 자동으로 생성되므로 최종 권한입니다.

· [Android C++ API용 C++ API 설명서 TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

각 Java 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 JavaDoc보다 더 많은 설명 자료가 포함되어 있으므로 Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.

· 마이그레이션 안내서 ([Android용 TVSDK 2.4 마이그레이션 안내서](../migration-guides/tvsdk-14-25-android.md))

이 안내서에서는 TVSDK 1.4 기반의 응용 프로그램을 TVSDK 2.4 기반의 응용 프로그램으로 마이그레이션하기 위해 수정해야 하는 사항에 대해 설명합니다.

## 새로운 기능 {#new-features}

Android용 TVSDK 2.4.1은 이전 버전보다 많은 성능 향상을 제공합니다. 고품질 시청 경험을 제공합니다.

이 버전에는 버전 2.4 및 2.4.1의 모든 기능이 포함되어 있으며 더 이상 사용되지 않는 기능은 없습니다.

버전 2.4.1의 새로운 주요 기능은 다음과 같습니다.

* HLS 버전 4 기능

   * **비디오 재생** 라이브, 선형 및 VOD 스트림에 대한 플레이어 컨트롤을 사용하여 (재생, 일시 중지, 찾기)
   * **자막** TVSDK는 608/708 폐쇄 캡션을 다양한 글꼴, 글꼴 크기, 색상 및 배경과 함께 표시할 수 있습니다. 또한 롤업 캡션이 있는 비디오를 지원하고 사용 가능한 경우 언어 트랙 간에 전환할 수 있습니다.
   * **트릭 재생 모드** 는 I-Frame을 사용하는 HLS 스트림에 대해 앞으로 감기 및 되감기를 지원합니다. 모든 비디오 재생 컨트롤은 콘텐츠에서 작동합니다. 속도가 0과 1 사이인 외부 비디오 재생 모드에서 슬로우 모션(앞으로)을 사용할 수 있습니다.
   * **적응형 비트율(ABR)** 은 플레이어가 네트워크 및 기타 조건에 따라 동일한 콘텐츠 스트림의 여러 버전 중 재생할 버전을 동적으로 선택할 수 있도록 해줍니다. 동적으로 또는 매니페스트 파일에서 매개 변수를 설정하여 적극적, 중간 및 보존적 선택 정책 중에서 선택할 수 있습니다.
   * **바이트 범위** 단일 TS 파일에 여러 TS 세그먼트를 포함할 수 있도록 합니다.
   * **대체 오디오 렌디션** 플레이어에서 사용 가능한 오디오 트랙 간을 전환할 수 있도록 합니다.
   * **ID3 지원.** TVSDK는 아티스트 이름, 제목 및 앨범과 같은 ID3 오디오 메타데이터가 포함된 HLS 오디오 및 비디오 스트림을 재생할 수 있습니다.
   * **장애 조치(failover). **TVSDK는 호스트 서버, 재생 목록 파일 및 세그먼트의 실패에도 불구하고 중단 없는 재생을 계속하기 위해 전략을 사용합니다.
   * **멀티채널 오디오 패스스루(DD+)** TVSDK는 Dolby Digital Plus 오디오(E-AC3) 데이터를 지원 하드웨어로 전달할 수 있습니다.

* 콘텐츠 보호 기능

   * **HLS용 DRM** 모든 비디오 재생 API는 Adobe 액세스로 보호되는 암호화된 비디오 콘텐츠와 함께 작동합니다. 지원되는 DRM 기능은 다음과 같습니다.

      * 라이선스 회전
      * 키 회전
      * 라이선스 캐싱
      * 정책 시간
      * IV 회전

* **AES 128 재생.** TVSDK는 키 크기가 128비트인 AES(고급 암호화 표준) HLS 콘텐츠를 재생할 수 있습니다.
* **보호된 HLS(PHLS)** 는 라이브 및 VOD 스트림에 대해 HLS를 통해 경량 DRM을 활성화할 수 있도록 Adobe 액세스가 제공하는 정책의 하위 집합인 사전 설치된 DRM 정책 세트를 제공합니다.

* 광고/대체 콘텐츠 및 수익 창출 기능

   * **서버측 삽입 광고 추적.** TVSDK는 Adobe 클라우드 광고 삽입 서비스에서 삽입한 광고를 추적할 수 있습니다. VOD 및 라이브/선형 스트림에 대한 VAST2, VAST3 및 VMAP 형식의 선형 광고를 지원합니다.
   * **사용자 지정 HLS 태그입니다.** TVSDK는 `MediaPlayerConfig` 사용자 지정 HLS 태그가 스트림에 표시되는 경우 플레이어 응용 프로그램에 알리는 기능을 활성화하는 클래스입니다.
   * **클라이언트측 광고 삽입.** Auditude 광고 삽입 라이브러리는 Adobe Auditude 서버와 함께 작동하여 프리롤, 미드롤 또는 포스트롤 위치에서 라이브, 선형 및 VOD 콘텐츠에 삽입하기 위한 광고를 동적으로 분석합니다.
   * **사용자 지정 광고 해결자입니다.** 다음 `ContentResolver, OpportunityGenerator,` 및 `MediaPlayerClientFactory` 인터페이스를 사용하면 사용자 지정 광고/대체 콘텐츠 확인자를 구현하고 TVSDK에서 작동하도록 사용자 지정 기회 감지기를 등록할 수 있습니다. 다음 `TestAdResolver` 및 `AuditudeResolver` 클래스는 content resolver 구현의 C++ 예를 제공합니다. 다음에서 Javascript 예를 찾을 수 있습니다. `samples/jspsdk/testapp/psdk.js`.
   * **일관된 광고 동작.** 사용 `AdPolicySelector` 콘텐츠에 광고가 있을 때 찾기 및 트릭 플레이와 같은 작업에 대해 모든 플레이어에서 일관된 동작을 사용할 수 있도록 하는 인터페이스입니다. 자체 구현을 하지 않는 경우 TVSDK는 `DefaultAdPolicySelector`.
   * **C3 광고 제거/바꾸기** 적절한 TVSDK API를 사용하여 사용자 지정 콘텐츠 범위를 제거하고 추가 준비 작업 없이 새 광고를 동적으로 삽입합니다. 이 기능은 라이브/선형 콘텐츠가 브로드캐스트되고 정리 없이 즉시 필요할 때 사용할 수 있어 편리합니다.

새로운 주요 기능 버전 2.4는 다음과 같습니다.

* **VOD 및 라이브를 즉시 실행** 인스턴트 온 기능을 활성화하면 재생이 시작되기 전에 TVSDK가 미디어를 초기화하고 버퍼링합니다. 여러 개의 를 실행할 수 있으므로 `MediaPlayerItemLoader` 인스턴스는 백그라운드에서 동시에 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서의 재생이 즉시 시작됩니다. TVSDK 2.4는 라이브 스트림에 대해서도 Instant On을 지원합니다. 라이브 스트림은 라이브 창이 이동할 때 다시 버퍼링됩니다.

* **성능 개선**새로운 TVSDK 2.4 아키텍처는 다음과 같이 다양한 성능 개선 사항을 제공합니다.

   * **하위 세분화** - TVSDK는 가능한 한 빨리 재생을 시작하기 위해 각 조각의 크기를 더 줄입니다.
   * **병렬 광고 다운로드** - TVSDK는 광고 브레이크를 누르기 전에 컨텐츠 재생과 동시에 광고를 미리 가져와서 광고 및 컨텐츠를 원활하게 재생할 수 있습니다.
   * **지연 광고 해결** - 이 기능을 사용하면 재생을 시작하기 전에 프리롤이 아닌 광고의 해상도를 기다리지 않으므로 시작 시간이 줄어듭니다. 찾기 및 트릭 플레이와 같은 API는 모든 광고가 해결될 때까지 계속 허용되지 않습니다.

* **MP4 컨텐츠 재생**

이 버전의 TVSDK는 MP4를 기본 콘텐츠로 재생할 수 있습니다.

* **영구 네트워크 연결**

TVSDK는 재사용 가능한 네트워크 연결 집합을 유지 관리하므로 각 네트워크 요청에 대한 네트워크 연결을 만들고 삭제하는 오버헤드가 발생하지 않습니다.

* **해상도 기반 출력 보호**

이 기능은 재생 제한을 특정 해상도에 연결하여 보다 세밀한 DRM 컨트롤을 제공합니다.

* **적응형 비트 전송률(ABR)을 사용한 트릭 플레이**

이 기능을 사용하면 TVSDK가 트릭 재생 모드에 있는 동안 iFrame 스트림 간을 전환할 수 있습니다. iFrame 이외의 프로필을 사용하여 더 낮은 속도에서 트릭 플레이를 수행할 수 있습니다.

* **매끄러운 트릭 플레이**

이러한 개선 사항은 사용자 경험을 향상시킵니다.

· 대역폭 및 버퍼 프로필을 기반으로 트릭 플레이 중 적응형 비트 전송률 및 프레임 전송률 선택

· IDR 스트림 대신 주 스트림을 사용하여 최대 30fps 고속 재생을 수행합니다.

* **향상된 ABR 논리**

새로운 ABR 논리는 버퍼 길이, 버퍼 길이 변경률 및 측정된 대역폭을 기반으로 합니다. 이렇게 하면 ABR에서 대역폭이 변동할 때 올바른 비트율을 선택하고 버퍼 길이가 변하는 속도를 모니터링하여 비트율 전환이 실제로 발생하는 횟수를 최적화합니다.

* **청구**

TVSDK는 고객 판매 계약을 준수하여 지표를 자동으로 수집하여 청구 목적에 필요한 주기적 사용 보고서를 생성합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림의 기간에 따라 콘텐츠 유형, 광고 삽입 활성화 플래그 및 drm 활성화 플래그와 같은 청구 지표를 Adobe Analytics Primetime 소유 보고서 세트에 보냅니다. 이 경우 고객의 자체 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하거나 여기에 포함되지 않습니다. 요청 시 이 청구 사용 보고서는 정기적으로 고객에게 전송됩니다. 사용량 청구만 지원하는 청구 기능의 첫 번째 단계입니다. 설명서에 설명된 API를 사용하여 판매 계약을 기반으로 구성할 수 있습니다.

## 지원되는 기능 {#supported-features}

Android 2.4용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 기능을 지원합니다.

>[!NOTE]
>
>아래 기능 매트릭스 표에서 는 √이 현재 릴리스에서 지원됨을 의미합니다.

### 코어 재생 기능 {#core-playback-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| 일반 재생(재생, 일시 중지, 찾기) | VOD + 라이브 | √ | √(VOD만 해당) |
| FER - 일반 재생(재생, 일시 중지, 찾기) | VOD 재생 | √ | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | √ | √ |
| 적응 비트 전송률 전환 논리 | VOD + 라이브 | √ | 지원되지 않음 |
| 오디오 전용 재생 | VOD + 라이브 | √ | 지원되지 않음 |
| 폐쇄 캡션 - 608/708 | VOD + 라이브 | √ | √(VOD만 해당) |
| 폐쇄 캡션 - WebVTT | VOD + 라이브 | √ | √(VOD만 해당) |
| 매니페스트 장애 조치 | VOD + 라이브 | √ | √(VOD만 해당) |
| 고급 페일오버 | VOD + 라이브 | √ | √(VOD만 해당) |
| QoS 및 플레이어 알림 | VOD + 라이브 | √ | √(VOD만 해당) |
| 쿠키 헤더 지원 | VOD + 라이브 | √ | √(VOD만 해당) |
| 사용자 지정 헤더 지원 | VOD + 라이브 | 지원되지 않음 | 지원되지 않음 |
| 버퍼 제어 매개 변수 설정 | VOD + 라이브 | √ | √(VOD만 해당) |
| 적응형 비트 전송률 제어 설정 | VOD + 라이브 | √ | √(VOD만 해당) |
| 사용자 지정 매니페스트 태그(HLS) / 이벤트 스트림(DASH) | VOD + 라이브 | √ | √(VOD만 해당) |
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
   <td>오프셋이 있는 재생</td> 
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
   <td>부드러운 트릭 플레이(ABR 포함)</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>ID3 구문 분석(HLS) / 시간 메타데이터(DASH)</td> 
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
   <td>즉시 사용</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>불연속 마커 지원(HLS) </li> 
     <li>다중 기간(대시)</li> 
    </ul> </td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>302 리디렉션 고정</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD만 해당)</td> 
  </tr>
  <tr>
   <td>썸네일 스크러빙(Iframe 및 JPEG)</td> 
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
| 일반 재생, 광고 활성화됨 | VOD + 라이브 | √ | √(VOD 프리롤만 해당) |
| 광고가 활성화된 FER 콘텐츠 | VOD | √ | 지원되지 않음 |
| 기본 광고 동작 | VOD + 라이브 | √ | √(VOD 프리롤만 해당) |
| VAST 2.0/3.0 | VOD + 라이브 | √ | √(VOD 프리롤만 해당) |
| VMAP 1.0 | VOD + 라이브 | √ | √(VOD 프리롤만 해당) |
| MP4 광고 | VOD + 라이브 | √(CRS에서) | √(CRS에서, 사전 롤만 해당) |

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
   <td>광고가 활성화된 트릭 플레이</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>광고만 </td> 
   <td>VOD</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>타깃팅 매개 변수</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만 해당)</td> 
  </tr>
  <tr>
   <td>사용자 지정 매개 변수</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만 해당)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 동작</td> 
   <td>VOD + 라이브</td> 
   <td>√</td> 
   <td>√(VOD 프리롤만 해당)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 태그</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 해결자</td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>Freewheel 사용자 지정 광고 해결 프로그램</td> 
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
   <td>지연 광고 로드</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>불연속 마커 지원 - SSAI (HLS) </li> 
     <li>다중 기간(대시)</li> 
    </ul> </td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>컴패니언 광고, 배너 광고 및 클릭 가능한 광고</td> 
   <td>VOD + 라이브</td> 
   <td>√ </td> 
   <td>√(VOD 프리롤만 해당)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + 라이브</td> 
   <td>√(JS) </td> 
   <td>√(VOD 프리롤만 해당)</td> 
  </tr>
  <tr>
   <td>초기 광고 종료</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>규칙 기반 Creative VOD + 라이브 우선 순위 지정</td> 
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

## 컨텐츠 보호 기능 {#content-protection-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| AES 암호화 | VOD + 라이브 | √ | √(VOD만 해당) |
| 샘플 AES 암호화 | VOD + 라이브 | √ |  |
| 토큰화된 스트림 | VOD + 라이브 | √ |  |
| DRM | VOD + 라이브 | Primetime DRM만 해당(향후: Widevine) | Widevine만 |
| 외부 재생(RBOP) | VOD + 라이브 | Primetime DRM 전용 | 지원되지 않음 |
| 라이선스 회전 | VOD + 라이브 | Primetime DRM 전용 | 지원되지 않음 |
| 키 회전 | VOD + 라이브 | Primetime DRM 전용 | 지원되지 않음 |

### 통합 기능 {#integration-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| Adobe Analytics VHL 통합 | VOD + 라이브 | √ | √ |
| 청구 | VOD + 라이브 | √ | 지원되지 않음 |

## 지원되지 않는 기능 {#features-not-supported}

이 버전의 TVSDK는 다음을 지원하지 않습니다.

* 광고 일시 중단.
* 트릭 플레이에서 슬로우 모션입니다.
* MP4 콘텐츠로 찾기 및 트리크플레이
* MP4 주 콘텐츠로 광고 삽입.
* 광고가 재생될 때 찾습니다.
* 오디오 전용 미디어가 있는 광고 재생.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 장치별 (Samsung Galaxy Tab 4) 충돌 VOD DRM LBA 와 함께 감사 및 클릭 광고
* 포스트롤 광고는 특정 콘텐츠에 대해 재생되지 않습니다.
* 닫기 캡션을 한중일 언어로 설정하면 작동하지 않습니다.
* VOD와 라이브 중에 비디오가 자동으로 트릭 모드에서 나올 수 있습니다.
* VHL - 오프셋에서 콘텐츠를 시작하면 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생될 때 이벤트에 대한 VHL 하트비트 호출:type:재생 광고가 누락되었습니다.
* adBreakPolicy SKIP을 선택한 경우에도 프리롤 광고가 재생됩니다.
* 완료 상태로 전환하면 플레이어가 포스트롤 광고에 대한 SKIP adBreakPolicy를 사용하여 재생 상태로 돌아갑니다.

비디오가 없으면 뷰포트 차원이 없고 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
