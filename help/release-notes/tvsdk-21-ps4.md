---
title: TVSDK 2.1 PlayStation 4 릴리스 정보
seo-title: TVSDK 2.1 PlayStation 4 릴리스 정보
description: PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제를 설명합니다.
seo-description: PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제를 설명합니다.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# TVSDK 2.1 PlayStation 4 릴리스 노트 {#tvsdk-playstation-release-notes}

PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제를 설명합니다.

## 해결된 문제 {#resolved-issues}

다음은 PlayStation 4용 TVSDK 2.1의 해결된 문제입니다.

**버전 2.1.0.638**

* **PTPLAY-10439:**
VMAP 래퍼 광고 링크가 끊어진 경우 플레이어가 준비 상태에 고정되었습니다(전송하지 않음). 
`onComplete` 발신자 참조).

* **PTPLAY-10179:**

   `creativeRepackaging` 및  `fallbackOnInvalidCreative` 값은 이제 기본적으로 꺼져 있습니다. 또한 `creativeRepackaging` 플래그가 설정되었지만 `creativeRepackaging` 형식이 제공되지 않은 경우 광고 중단에 광고가 있는 횟수만큼 `onRepackagingComplete`이(가) 호출되어 광고 중단이 여러 번 생성되었습니다.

* **Zendesk #10304**:광고 형식/해제 변수가 초기화되지 않았습니다. 이제 `DataSetEntry's` 센터에서 변수를 초기화합니다.

* **PTPLAY-10318: 배경**
모드에 대한 지원이 도입되었습니다.
* **Zendesk # 17409:**
트릭 재생 모드로 전환한 다음 일반 재생 모드로 다시 돌아가 트릭 재생 모드로 전환하면 재생 위치가 이동하는 것이었습니다.
* **PTPLAY-9552: 응답 XML 파일을 구문**
분석한 후 광고가 없을 때마다 오류 코드 1108이 핑됩니다.
* **PTPLAY-9551:**
Auditude 처리 후 광고 중단이 없으면 CRS가 
**** onPrefetchComplete를 통해 groupCount를 감소시킵니다. 광고 브레이크가 없으므로 **groupCount**&#x200B;는 0이고 1만큼 감소합니다. 이전에는 **groupCount**&#x200B;는 최대 값으로 변경하는 데 사용되었기 때문에 **uint32_t**&#x200B;이었습니다. 이제 **int32_t**&#x200B;입니다.

**버전 2.1.0.621**

* **Zendesk #4555**
Instant on Memory issues leading-Loading errors - 
`MediaItemLoader` 출시 중 충돌 발생 수정  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI:일부 광고 추적 URL이 실행되지 않음
   * 인라인 광고를 가리키는 일부 VAST 광고가 추적 URL을 누락했습니다.
   * VAST XML의 광고에 노출 태그가 여러 개 있는 경우 첫 번째 노출 url만 저장되고 나머지는 무시됩니다. 이제 모든 노출 URL이 저장되고 나중에 핑됩니다.
* **Zendesk #17224**
PS4 사용자 에이전트, primetime 정보를 UAString 끝으로 이동
* **Zendesk #17226**
2.x CSAI:일부 광고는 이에 첨부되지 않았다.
\
   insertBy 또는 eraseBy 작업으로 인해 타임라인이 변경되었음을 알리고 이에 따라 기간 전환을 수행합니다.

* **Zendesk #17284**
   [모든 ] 플랫폼자막이 표시되지 않습니다.\
   HLS - VTT 캡션 파일에 대한 `EXT-X-MEDIA-TIME` 태그를 지원합니다.

* **PS4의 Zendesk #17889**
Playback &quot;Milk&quot;
\
   올바른 윤곽 적용(색상 변환용)

* **Zendesk #17954**
광고 폴백 논리 + 빈 광활한 처리
\
   Vast 래퍼 중 하나가 비어 있는 경우 Vast 구문 분석기가 래퍼를 계속 처리하는 데 사용되던 문제를 수정했습니다.

* **Zendesk #17807**
비어 있는 광대한 곳을 넘을 수 없습니다 Zendesk #3103과 동일합니다.

* **Zendesk #17865**
PS4 및 XBox One의 폴백 로직
\
   Zendesk #3103과 동일

**버전 2.1.0.591**

* **Zendesk #3767**
PS4 광고 코드 조각, VMAP 리디렉션 처리 시 광고 문제 해결
* **Zendesk #4096**
PS4 CSAI:세그멘테이션 오류 광고 라이브러리가 VMAP 응답을 처리할 때 TVSDK에서 세그멘테이션 오류가 발생하는 문제를 해결했습니다.

* **Zendesk #4161**
Trickplay 16x무비 끝 시 멈추기 트릭플레이가 일반 재생으로 돌아갈 때 발생하는 교착 상태가 해결되었습니다.

* **자막이 활성화되어**
있는 Zendesk #4208자막의 임의 충돌

* **Zendesk #4213**
PS4 CSAI:모든 광고 관련 호출에 대한 기본 사용자-에이전트 문자열 변경 + Primetime 문자열을 사용하는 브라우저와 동일한 UA 문자열을 사용하여 사용자-에이전트 문자열이 만들어집니다

* **PTPLAY-7675** (내부) 코드 변환된 광고가 VMAP 또는 VAST 응답 내에서 호출될 때 크리에이티브 재패키징을 재생하지 못했습니다. 광고 규모가 큰 경우 자산에서 읽는 대신 광고에서 미디어를 읽을 수 있도록 수정되었습니다.

* **PTPLAY-7895** (내부)  `allowMultipleAds=false`메시지가 올바르게 표시되지 않는 고정 버그가  `allowMultipleAds` 광고되지 않는 경우

* **PTPLAY-7896** (내부) 광고가 XML 응답에 표시된 순서로 광고가 표시되지 않는 PS4 고정 문제에 대해 광고가 순서 반대로 재생되고 있습니다.

* PS4 TV SDK는 게임이 아닌 미니 앱 내에서 재테스트되었습니다.

**버전 2.1.0.563**

* **Zendesk #3868**
TVSDK는 Playstation SDK 2.5를 지원합니까? TVSDK는 현재 2.5 Playstation SDK로 빌드됩니다.

* **Zendesk #4093**
targetingPt 광고 요청의 정보 키-값 쌍.
\
   키/값 쌍을 구분하는 줄바꿈 문자가 추가되었습니다.

## 지원되는 기능 {#supported-features}

PlayStation 4용 TVSDK 2.1에서는 다음 기능이 지원됩니다.

**버전 2.1.0.621**

* 광고 폴백, 광고 선택 로직의 데이지 체인(Zendesk #3103)
폴백 규칙이 활성화된 VAST 광고(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용하려고 시도합니다.폴백 동작의 일부 측면을 구성할 수 있습니다

**버전 2.1.0.538**

* 재생, 일시 정지, 검색 등 HLS VOD 재생
* 적응형 비트 전송률 스트리밍
* Primetime DRM 및 바닐라 AES로 보호된 콘텐츠를 통해 암호화된 컨텐츠 재생
* 기본 광고 비헤이비어 및 광고 용서를 사용하는 클라이언트측 광고 삽입
* 크리에이티브한 리패키징
* WebVTT 자막
* 사용자 정의 시작 위치로 즉시 사용
* 빨리 감기 및 빨리 되감기로 속기
* 302 리디렉션

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 문서를 참조하십시오.