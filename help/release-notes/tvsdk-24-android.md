---
title: Android용 TVSDK 2.4.1 릴리스 노트
description: Android용 TVSDK 2.4.1 릴리스 노트에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Android용 TVSDK 2.4.1 릴리스 노트 {#tvsdk-for-android-release-notes}

Android용 TVSDK 2.4.1 릴리스 노트에서는 TVSDK Android 2.4.1의 새로운 기능 및 지원되는 기능과 알려진 문제 및 제한 사항에 대해 설명합니다.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe이 Android용 TVSDK 2.4.1을 출시하고 있습니다.

이 버전의 TVSDK를 사용하려면 시스템이 [시스템 요구 사항](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

다음은 설명서를 찾을 수 있는 위치입니다.

・ Android용 온라인 도움말 시스템 TVSDK 2.4 도움말

・ [Android Java API용 Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs는 TVSDK 소스 코드에서 직접 자동으로 생성되므로 최종 권위입니다.

・ [Android C++ API용 C++ API 설명서 TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

각 Java 클래스에는 해당 C++ 클래스가 있으며, C++ 설명서에는 Javadocs보다 더 많은 설명 자료가 포함되어 있으므로 Java API에 대한 자세한 내용은 C++ 설명서를 참조하십시오.

・ 마이그레이션 안내서([Android용 TVSDK 2.4 마이그레이션 안내서](../migration-guides/tvsdk-14-25-android.md))

이 안내서에서는 TVSDK 1.4를 기반으로 하는 애플리케이션을 TVSDK 2.4를 기반으로 한 애플리케이션으로 마이그레이션하기 위해 수정해야 하는 사항을 설명합니다.

## 새로운 기능 {#new-features}

Android용 TVSDK 2.4.1은 이전 버전보다 향상된 성능을 제공합니다. 고품질 보기 환경을 제공합니다.

이 버전에는 버전 2.4 및 2.4.1의 모든 기능이 포함되어 있으며 더 이상 사용되지 않는 기능이 없습니다.

버전 2.4.1의 새로운 주요 기능은 다음과 같습니다.

* HLS 버전 4 기능

   * **비디오 재생** (재생, 일시 정지, 찾기) 플레이어 제어를 사용하여 라이브, 선형 및 VOD 스트림을 생성합니다.
   * **자막.** TVSDK는 글꼴, 글꼴 크기, 색상 및 배경에서 608/708 자막을 표시할 수 있습니다. 또한 롤업 캡션이 포함된 비디오를 지원하고 언어 추적 간에 전환할 수 있습니다.
   * **트릭 재생 모드** 는 I-Frame을 사용하는 HLS 스트림에 대해 앞으로 감기 및 되감기를 지원합니다. 모든 비디오 재생 컨트롤은 컨텐츠에서 작동합니다. 0에서 1 사이의 비율로 외부 비디오 재생 모드에 대해 느린 동작(앞으로)을 사용할 수 있습니다.
   * **적응형 비트율(ABR)** 플레이어에서 네트워크 및 기타 조건에 따라 동일한 컨텐츠 스트림의 여러 버전 중 재생할 버전을 동적으로 선택할 수 있습니다. 동적으로 또는 매니페스트 파일에서 매개 변수를 설정하여 공격적이고, 중적이며, 보수적인 선택 정책 중에서 선택할 수 있습니다.
   * **바이트 범위** 여러 TS 세그먼트를 포함하려면 단일 TS 파일을 활성화하십시오.
   * **대체 오디오 표현물** 플레이어에서 사용 가능한 오디오 트랙 간을 전환할 수 있도록 설정.
   * **ID3 지원.** TVSDK는 아티스트 이름, 제목 및 앨범과 같은 ID3 오디오 메타데이터가 포함된 HLS 오디오 및 비디오 스트림을 재생할 수 있습니다.
   * **장애 조치(failover). **TVSDK는 호스트 서버, 재생 목록 파일 및 세그먼트가 실패하더라도 중단되지 않은 재생을 계속하기 위한 전략을 사용합니다.
   * **다중 채널 오디오 패스스루(DD+).** TVSDK는 Dolby Digital Plus 오디오(E-AC3) 데이터를 지원 하드웨어에 전달할 수 있습니다.

* 컨텐츠 보호 기능

   * **HLS용 DRM.** 모든 비디오 재생 API는 Adobe 액세스로 보호되는 암호화된 비디오 콘텐츠와 연동합니다. 지원되는 DRM 기능은 다음과 같습니다.

      * 라이선스 순환
      * 키 순환
      * 라이선스 캐싱
      * 정책 시간
      * IV 회전

* **AES 128 재생.** TVSDK는 키 크기가 128비트인 AES(고급 암호화 표준) HLS 컨텐츠를 재생할 수 있습니다.
* **보호된 HLS(PHLS)** 에서는 라이브 및 VOD 스트림에 대해 HLS를 통해 경량 DRM을 활성화할 수 있도록 Adobe 액세스의 하위 집합인 미리 빌드된 DRM 정책 집합 제한을 제공합니다.

* 광고/대체 컨텐츠 및 수익 창출 기능

   * **서버측에서 삽입된 광고에 대한 추적.** TVSDK는 Adobe 클라우드 광고 삽입 서비스에서 삽입한 광고를 추적할 수 있습니다. VOD 및 라이브/선형 스트림에 대해 VAST2, VAST3 및 VMAP 포맷의 선형 광고를 지원합니다.
   * **사용자 지정 HLS 태그.** TVSDK에서는 다음을 사용합니다 `MediaPlayerConfig` 사용자 지정 HLS 태그가 스트림에 표시될 때 플레이어 애플리케이션에 알릴 수 있는 클래스입니다.
   * **클라이언트 측 광고 삽입.** Auditude 광고 삽입 라이브러리는 Adobe Auditude 서버와 함께 프리롤, 미드롤 또는 포스트롤 위치에서 라이브, 선형 및 VOD 컨텐츠에 동적으로 삽입되는 광고를 해결합니다.
   * **사용자 지정 광고 해상도.** 다음 `ContentResolver, OpportunityGenerator,` 및 `MediaPlayerClientFactory` 인터페이스를 사용하면 사용자 지정 광고/대체 컨텐츠 확인자를 구현하고 TVSDK에서 작업할 수 있도록 사용자 지정 기회 감지기를 등록할 수 있습니다. 다음 `TestAdResolver` 및 `AuditudeResolver` 클래스는 content resolver를 구현하는 C++ 예를 제공합니다. 에서 Javascript 예를 찾을 수 있습니다. `samples/jspsdk/testapp/psdk.js`.
   * **일관된 광고 동작입니다.** 를 사용하십시오 `AdPolicySelector` 광고가 컨텐츠에 있을 때 찾기 및 트릭 플레이와 같은 작업에 대해 모든 플레이어에서 일관된 동작을 가능하게 하는 인터페이스. 자체 구현하지 않는 경우 TVSDK는 를 사용합니다 `DefaultAdPolicySelector`.
   * **C3 광고 제거/바꾸기** 적절한 TVSDK API를 사용하여 사용자 지정 콘텐츠 범위를 제거하고 추가 준비 작업 없이 새 광고를 동적으로 삽입합니다. 이 기능은 라이브/선형 컨텐츠가 브로드캐스트되고 정리 없이 즉시 주문형 사용 가능하게 될 때 유용합니다.

다음은 버전 2.4의 주요 새로운 기능입니다.

* **VOD 및 라이브를 위한 즉각적인 설정** 인스턴트 온(instant on) 을 활성화하면 TVSDK가 미디어를 초기화하고 버퍼링한 후 재생이 시작됩니다. 여러 번 실행할 수 있으므로 `MediaPlayerItemLoader` 인스턴스는 백그라운드에서 동시에 여러 스트림을 버퍼링할 수 있습니다. 사용자가 채널을 변경하고 스트림이 제대로 버퍼링되면 새 채널에서 재생이 즉시 시작됩니다. TVSDK 2.4는 라이브 스트림용 인스턴트 온도 지원합니다. 라이브 창이 이동하면 라이브 스트림이 다시 버퍼링됩니다.

* **성능 개선 **새로운 TVSDK 2.4 아키텍처는 다음과 같이 다양한 성능 개선 사항을 제공합니다.

   * **하위 세그먼테이션** - TVSDK는 가능한 한 빨리 재생을 시작할 각 조각의 크기를 더 줄입니다.
   * **병렬 광고 다운로드** - TVSDK는 광고 브레이크에 도달하기 전에 컨텐츠 재생과 동시에 광고를 미리 가져오기 때문에 광고 및 컨텐츠를 원활하게 재생할 수 있습니다.
   * **레이지 광고 해상도** - 이 기능을 사용하여 재생을 시작하기 전에 프리롤 광고가 아닌 광고의 해상도를 기다리지 않으므로 시작 시간이 줄어듭니다. 모든 광고가 해결될 때까지 검색 및 트릭 플레이와 같은 API는 계속 허용되지 않습니다.

* **MP4 컨텐츠 재생**

이 버전의 TVSDK는 MP4 재생을 기본 컨텐츠로 지원합니다.

* **영구 네트워크 연결**

TVSDK는 재사용 가능한 네트워크 연결 집합을 유지 관리하므로 각 네트워크 요청에 대해 네트워크 연결을 만들고 삭제하는 오버헤드가 발생하지 않습니다.

* **해상도 기반의 출력 보호**

이 기능은 재생 제한을 특정 해상도에 연결하여 보다 세밀하게 조정된 DRM 컨트롤을 제공합니다.

* **응용 비트 전송률(ABR)로 트릭 재생**

이 기능을 사용하면 TVSDK가 트릭 재생 모드에서 iFrame 스트림 간을 전환할 수 있습니다. iFrame이 아닌 프로필을 사용하여 빠른 속도로 트릭 재생을 수행할 수 있습니다.

* **더 원활한 트릭 재생**

이러한 개선 사항은 사용자 경험을 향상시킵니다.

・ 대역폭 및 버퍼 프로파일을 기반으로 트릭 재생 중 적응형 비트율 및 프레임 속도 선택

・ IDR 스트림 대신 기본 스트림을 사용하여 최대 30fps의 빠른 재생을 지원합니다.

* **향상된 ABR 논리**

새로운 ABR 로직은 버퍼 길이, 버퍼 길이 변경 속도 및 측정된 대역폭을 기반으로 합니다. 이렇게 하면 ABR에서 대역폭이 변경될 때 올바른 비트 전송률을 선택하고 버퍼 길이가 변경되는 속도를 모니터링하여 비트율 스위치가 실제로 발생하는 횟수를 최적화합니다.

* **과금**

TVSDK는 고객 판매 계약을 준수하여 자동으로 지표를 수집하여 청구 용도로 필요한 주기적 사용량 보고서를 생성합니다. 모든 스트림 시작 이벤트에서 TVSDK는 Adobe Analytics 데이터 삽입 API를 사용하여 청구 가능한 스트림 기간을 기반으로 컨텐츠 유형, 광고 삽입 활성화 플래그 및 drm 지원 플래그와 같은 청구 지표를 Adobe Analytics Primetime 소유 보고서 세트에 보냅니다. 이는 고객의 Adobe Analytics 보고서 세트 또는 서버 호출을 방해하지 않거나 분석에 포함되지 않습니다. 요청 시 이 청구 사용량 보고서는 고객에게 정기적으로 전송됩니다. 사용 과금만 지원하는 청구 기능의 첫 번째 단계입니다. 설명서에 설명된 API를 사용하여 판매 계약에 따라 구성할 수 있습니다.

## 지원되는 기능 {#supported-features}

Android 2.4용 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 많은 기능을 지원합니다.

>[!NOTE]
>
>아래 기능 매트릭스 테이블에서 √은 기능이 현재 릴리스에서 지원됨을 의미합니다.

### 코어 재생 기능 {#core-playback-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| 일반 재생(재생, 일시 정지, 찾기) | VOD + Live | √ | √ (VOD만 해당) |
| FER - 일반 재생(재생, 일시 중지, 검색) | VOD 전송 | √ | 지원되지 않음 |
| MP3 | VOD | 지원되지 않음 | 지원되지 않음 |
| MP4 컨텐츠 재생 | VOD | √ | √ |
| 응용 비트율 전환 논리 | VOD + Live | √ | 지원되지 않음 |
| 오디오 전용 재생 | VOD + Live | √ | 지원되지 않음 |
| 닫힘 캡션 - 608/708 | VOD + Live | √ | √ (VOD만 해당) |
| 닫힘 캡션 - WebVTT | VOD + Live | √ | √ (VOD만 해당) |
| 매니페스트 장애 조치(Failover) | VOD + Live | √ | √ (VOD만 해당) |
| 고급 페일오버 | VOD + Live | √ | √ (VOD만 해당) |
| QoS 및 플레이어 알림 | VOD + Live | √ | √ (VOD만 해당) |
| 쿠키 헤더 지원 | VOD + Live | √ | √ (VOD만 해당) |
| 사용자 지정 헤더 지원 | VOD + Live | 지원되지 않음 | 지원되지 않음 |
| 버퍼 제어 매개 변수 설정 | VOD + Live | √ | √ (VOD만 해당) |
| 적응형 비트율 컨트롤 설정 | VOD + Live | √ | √ (VOD만 해당) |
| 사용자 지정 매니페스트 태그(HLS)/이벤트 스트림(DASH) | VOD + Live | √ | √ (VOD만 해당) |
| 늦게 바인딩된 오디오 | VOD + Live | √ | √ (VOD만 해당) |
| 302 리디렉션 | VOD + Live | √ | √ (VOD만 해당) |

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
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>트릭 플레이 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>부드러운 트릭 재생(ABR 사용)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>ID3 구문 분석(HLS) / 시간 메타데이터(DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>일시 중단 </td> 
   <td>VOD + Live</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>즉시 켜기</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>HLS(무중단 마커 지원) </li> 
     <li>다기간(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>302 리디렉션 고착성</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (VOD만 해당)</td> 
  </tr>
  <tr>
   <td>축소판 스크러빙(Iframe 및 JPEG)</td> 
   <td>VOD + Live</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>스트림 무결성 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>지원되지 않음</td> 
  </tr>
 </tbody>
</table>

### 핵심 Ad Insertion 기능(CSAI) {#core-ad-insertion-features-csai}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| 일반 재생, 광고 활성화 | VOD + Live | √ | √(VOD 프리롤 전용) |
| 광고가 활성화된 FER 컨텐츠 | VOD | √ | 지원되지 않음 |
| 기본 광고 동작 | VOD + Live | √ | √(VOD 프리롤 전용) |
| VAST 2.0/3.0 | VOD + Live | √ | √(VOD 프리롤 전용) |
| VMAP 1.0 | VOD + Live | √ | √(VOD 프리롤 전용) |
| MP4 광고 | VOD + Live | √ (CRS에서) | √(CRS에서 프리롤 전용) |

### CSAI(고급 Ad Insertion 기능) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>기능</strong></td> 
   <td><strong>컨텐츠 유형</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>대시</strong></td> 
  </tr>
  <tr>
   <td>광고가 활성화된 트릭 재생</td> 
   <td>VOD + Live</td> 
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
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√(VOD 프리롤 전용)</td> 
  </tr>
  <tr>
   <td>사용자 지정 매개 변수</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√(VOD 프리롤 전용)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 동작</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√(VOD 프리롤 전용)</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 태그</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>사용자 지정 광고 해상도</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>Freewheel Custom Ad Resolver</td> 
   <td>VOD</td> 
   <td>지원되지 않음</td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>C3 광고 교체 </td> 
   <td>VOD + Live</td> 
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
     <li>불연속성 마커 지원 - SSSAI(HLS) </li> 
     <li>다기간(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>컴패니언 광고, 배너 광고 및 클릭 가능한 광고</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√(VOD 프리롤 전용)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√ (JS) </td> 
   <td>√(VOD 프리롤 전용)</td> 
  </tr>
  <tr>
   <td>조기 광고 종료</td> 
   <td>라이브</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>규칙 기반 Creative VOD + 라이브 우선 순위 지정</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
  <tr>
   <td>CRS 규칙 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>지원되지 않음</td> 
  </tr>
 </tbody>
</table>

## 컨텐츠 보호 기능 {#content-protection-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| AES 암호화 | VOD + Live | √ | √ (VOD만 해당) |
| 샘플 AES 암호화 | VOD + Live | √ |  |
| 토큰화된 스트림 | VOD + Live | √ |  |
| DRM | VOD + Live | Primetime DRM만 해당(향후: Widevine) | Widevine만 |
| 외부 재생(RBOP) | VOD + Live | Primetime DRM만 해당 | 지원되지 않음 |
| 라이선스 순환 | VOD + Live | Primetime DRM만 해당 | 지원되지 않음 |
| 키 회전 | VOD + Live | Primetime DRM만 해당 | 지원되지 않음 |

### 통합 기능 {#integration-features}

| **기능** | **컨텐츠 유형** | **HLS** | **대시** |
|---|---|---|---|
| Adobe Analytics VHL 통합 | VOD + Live | √ | √ |
| 과금 | VOD + Live | √ | 지원되지 않음 |

## 지원되지 않는 기능 {#features-not-supported}

이 버전의 TVSDK는 다음을 지원하지 않습니다.

* 광고 일시 중단.
* 트릭 플레이의 느린 동작.
* MP4 콘텐츠를 사용하여 찾기 및 트릭을 수행합니다.
* MP4 기본 콘텐츠를 사용한 광고 삽입.
* 광고가 재생될 때 찾습니다.
* 오디오 전용 미디어를 사용한 광고 재생.

## 알려진 문제 및 제한 사항 {#known-issues-and-limitations}

이 버전의 TVSDK에는 다음과 같은 문제가 있습니다.

* 장치별(삼성 갤럭시 탭 4) 감사 기능이 있는 VOD DRM LBA를 충돌시키고 광고를 클릭합니다
* 포스트롤 광고가 특정 컨텐츠에 대해 재생되지 않습니다.
* 닫기 캡션을 CJK 언어로 설정할 수 없습니다.
* 비디오는 VOD와 라이브 사이에 자동으로 트릭 모드에서 나타날 수 있습니다.
* VHL - 오프셋에서 컨텐츠를 시작할 때 잘못된 하트비트 호출이 전송됩니다.
* VPAID 광고가 재생될 때 이벤트에 대한 VHL 하트비트 호출:type:재생 광고가 누락되었습니다.
* adBreakPolicy SKIP를 선택한 경우에도 프리롤 광고가 재생됩니다.
* 완료 상태 플레이어로 이동한 후 포스트롤 광고에 대한 SKIP adBreakPolicy를 사용하여 재생 상태로 돌아갑니다.

비디오가 없으면 뷰포트 차원이 없으며 뷰포트 차원이 없으면 캡션에 대한 그래픽을 표시할 수 없습니다.

## 유용한 리소스 {#helpful-resources}

* 에서 전체 도움말 설명서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지.
