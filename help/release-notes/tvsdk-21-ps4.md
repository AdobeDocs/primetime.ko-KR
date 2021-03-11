---
title: TVSDK 2.1 PlayStation 4 릴리스 정보
description: PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제에 대해 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# TVSDK 2.1 PlayStation 4 릴리스 노트 {#tvsdk-playstation-release-notes}

PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제에 대해 설명합니다.

## 해결된 문제 {#resolved-issues}

다음은 PlayStation 4용 TVSDK 2.1의 해결된 문제입니다.

**버전 2.1.0.638**

* **PTPLAY-10439:**
VMAP 래퍼 광고 링크가 깨졌을 때 플레이어가 준비 상태에 고정되었습니다(전송하지 않음). 
`onComplete` 를 호출자에게 보내기).

* **PTPLAY-10179:**

   `creativeRepackaging` 및  `fallbackOnInvalidCreative` 값은 이제 기본적으로 꺼져 있습니다. 또한 `creativeRepackaging` 플래그가 설정되었지만 `creativeRepackaging` 형식이 제공되지 않은 경우 광고 중단에 광고가 있는 횟수만큼 `onRepackagingComplete`이(가) 호출되어 광고 중단이 여러 번 생성됩니다.

* **Zendesk #10304**:광고 형식/해제 변수가 초기화되지 않았습니다. 이제 `DataSetEntry's` 센터에서 변수를 초기화합니다.

* **PTPLAY-10318:**
배경 모드에 대한 지원이 도입되었습니다.
* **Zendesk # 17409:**
트릭 재생 모드로 전환한 다음 일반 재생 모드로 되돌아가 다시 트릭 재생 모드로 전환하면 재생 위치가 이동되었습니다.
* **PTPLAY-9552: 응답 XML 파일을 구문**
분석한 후 광고가 없을 때마다 오류 코드 1108이 핑됩니다.
* **PTPLAY-9551:**
Auditude 처리 후 광고 브레이크가 없으면 CRS가 
**onPrefetchComplete를** 통해 groupCount를 감소시킵니다. 광고 할당이 없으므로 **groupCount**&#x200B;는 0이고 1만큼 감소합니다. 이전에는 **groupCount**&#x200B;는 최대 값으로 변경하는 데 사용되었기 때문에 **uint32_t**&#x200B;이었습니다. 이제 **int32_t**&#x200B;입니다.

**버전 2.1.0.621**

* **Zendesk #4555**
메모리 관련 즉각적인 문제 선행 로딩 오류 - 
`MediaItemLoader` 출시 중 충돌 발생 수정  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI:일부 광고 추적 URL이 실행되지 않음
   * 인라인 광고를 가리키는 일부 VAST 광고가 추적 URL을 누락했습니다.
   * VAST XML에 광고에 노출 태그가 여러 개 있는 경우 첫 번째 노출 URL만 저장되고 나머지는 무시됩니다. 이제 모든 노출 URL이 저장되고 나중에 핑됩니다.
* **Zendesk #17224**
PS4 사용자 에이전트 - primetime 정보를 UAString 끝으로 이동
* **Zendesk #17226**
2.x CSAI:일부 광고는 이에 포함됩니다.
\
   insertBy 또는 eraseBy 작업으로 인해 타임라인이 변경되었음을 표시하고 이에 따라 기간 전환을 수행하는 수정입니다.

* **Zendesk #17284**
   [모든 ] 플랫폼폐쇄 캡션이 표시되지 않습니다.\
   HLS - VTT 캡션 파일에 대한 `EXT-X-MEDIA-TIME` 태그를 지원합니다.

* **PS4의 Zendesk #17889**
재생 &quot;Milky&quot;
\
   올바른 설정 적용(색상 변환용)

* **Zendesk #17954**
광고 폴백 논리 + 빈 광대한 처리
\
   Vast 래퍼 중 하나가 비어 있는 경우 Vast 파서가 래퍼를 계속 처리하는 데 사용되던 문제를 수정했습니다.

* **Zendesk #17807**
빈 광대한 곳을 넘을 수 없습니다 Zendesk와 동일 #3103

* **Zendesk #17865**
PS4 및 XBox One의 폴백 로직
\
   Zendesk과 동일 #3103

**버전 2.1.0.591**

* **Zendesk #3767**
PS4 광고 코드 조각, VMAP 리디렉션을 처리할 때 광고 문제 해결 실패.
* **Zendesk #4096**
PS4 CSAI:세그멘테이션 오류 광고 라이브러리가 VMAP 응답을 처리할 때 TVSDK에서 세그멘테이션 오류가 발생하는 문제가 수정되었습니다.

* **무비 끝 부분에서 Zendesk #4161**
Trickplay 16x가 멈추는 속도 조작이 정상적인 재생으로 돌아갈 때 발생하는 교착 상태가 해결되었습니다.

* **닫힌 캡션이**
켜진 경우 Zendesk #4208 임의 충돌 닫힌 캡션이 활성화되면 메모리 누수가 수정됨

* **Zendesk #4213**
PS4 CSAI:모든 광고 관련 호출에 대한 기본 사용자-에이전트 문자열 변경

* **PTPLAY-7675** (내부) 코드 변환된 광고가 VMAP 또는 VAST 응답 내에서 호출될 때 크리에이티브 재패키징을 재생하지 못했습니다. 다양한 광고의 경우 자산에서 읽는 대신 광고에서 미디어를 읽는 것이 수정되었습니다.

* **PTPLAY-7895** (내부)  `allowMultipleAds=false`매개 변수를 올바르게 따르지 않는 고정 버그를  `allowMultipleAds` 광고하지 않는 경우.

* **PTPLAY-7896** (내부) 광고가 XML 응답에 광고가 표시되는 순서대로 표시되지 않는 문제가 해결되었습니다.

* PS4 TV SDK는 게임이 아닌 미니 앱 내에서 재테스트되었습니다.

**버전 2.1.0.563**

* **Zendesk #3868**
은 TVSDK가 Playstation SDK 2.5를 지원합니까? TVSDK는 현재 2.5 Playstation SDK로 구축되어 있습니다.

* **Zendesk #4093**
targetingPt 광고 요청의 Info 키-값 쌍.
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
* Primetime DRM 및 바닐라 AES로 보호된 콘텐츠로 암호화된 컨텐츠 재생
* 기본 광고 비헤이비어와 광고 용서가 포함된 클라이언트측 광고 삽입
* 크리에이티브한 리패키징
* WebVTT 자막
* 사용자 정의 시작 위치로 즉시 켜기
* 빨리 감기 및 빨리 되감기로 장난치기
* 302 리디렉션

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 설명서를 참조하십시오.