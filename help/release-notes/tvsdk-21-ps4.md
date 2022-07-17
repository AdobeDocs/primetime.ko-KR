---
title: TVSDK 2.1 PlayStation 4 릴리스 노트
description: PlayStation 4 릴리스 노트용 TVSDK 2.1 PlayStation 4 의 지원되는 기능과 알려진 문제에 대해 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# TVSDK 2.1 PlayStation 4 릴리스 노트 {#tvsdk-playstation-release-notes}

PlayStation 4 릴리스 노트용 TVSDK 2.1 PlayStation 4 의 지원되는 기능과 알려진 문제에 대해 설명합니다.

## 해결된 문제 {#resolved-issues}

다음은 PlayStation 4용 TVSDK 2.1에 대해 해결된 문제입니다.

**버전 2.1.0.638**

* **PTPLAY-10439:**
VMAP 래퍼 광고 링크가 끊기면 플레이어가 준비 상태에서 멈췄습니다(전송되지 않음) 
`onComplete` 발신자에게 전달).

* **PTPLAY-10179:**

   `creativeRepackaging` 및 `fallbackOnInvalidCreative` 이제 값이 기본적으로 꺼져 있습니다. 또한 `creativeRepackaging` 플래그가 설정되어 있지만 없음 `creativeRepackaging` 형식이 제공되었습니다. `onRepackagingComplete` 가 광고 브레이크에 광고가 있는 횟수만큼 호출되어 광고 브레이크가 여러 번 생성됩니다.

* **Zendesk #10304**: 광고 포텐션 온/오프 변수가 초기화되지 않았습니다. 이제 변수를 `DataSetEntry's` 톱니바퀴입니다.

* **PTPLAY-10318:**
배경 모드에 대한 지원이 도입되었습니다.
* **Zendesk # 17409:**
트릭 재생 모드로 전환한 다음 일반 재생 모드로 돌아간 다음 다시 트릭 재생 모드로 전환하면 재생 위치가 이동되었습니다.
* **PTPLAY-9552:**
응답 XML 파일을 구문 분석한 후 광고가 없을 때마다 오류 코드 1108이 ping됩니다.
* **PTPLAY-9551:**
Auditude 처리 후 광고 브레이크가 없으면 CRS가 호출합니다 
**onPrefetchComplete** groupCount가 감소합니다. 광고 브레이크가 없으므로 **groupCount** 는 0이고 1로 감소합니다. 이전 **groupCount** is **uint32_t** 왜냐하면 이 URL이 최대 값으로 변경되기 때문입니다. 이제 됐습니다 **int32_t**.

**버전 2.1.0.621**

* **Zendesk #4555**
메모리 시 즉각적인 문제로 인해 오류가 발생합니다. 
`MediaItemLoader` 릴리스 중 발생하는 충돌 수정 `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: 일부 광고 추적 URL이 실행되는 것은 아닙니다
   * 인라인 광고를 가리키는 일부 VAST 광고에 추적 URL이 누락되었습니다.
   * VAST XML의 광고에 노출 태그가 여러 개 있는 경우 첫 번째 노출 URL만 저장되고 나머지는 무시됩니다. 이제 모든 노출 URL이 저장되고 나중에 ping됩니다.
* **Zendesk #17224**
PS4 사용자 에이전트가 primetime 정보를 UAString의 끝으로 이동합니다.
* **Zendesk #17226**
2.x CSAI: 일부 광고에서 결합되지 않았습니다.
\
   [수정]은 insertBy 또는 eraseBy 작업으로 인해 타임라인이 변경되었음을 나타내고 그에 따라 기간 전환을 수행합니다.

* **Zendesk #17284**
   [모든 플랫폼] 닫힘 캡션이 표시되지 않습니다.\
   HLS - 지원 `EXT-X-MEDIA-TIME` 태그로 지정합니다.

* **Zendesk #17889**
PS4에서 &quot;Milky&quot; 재생
\
   올바른 설정(색상 변환용)이 적용되었습니다.

* **Zendesk #17954**
빈 vast를 처리하는 대체 논리 + 처리
\
   Vast 래퍼 중 하나가 비어 있는 경우 Vast 파서가 래퍼 처리를 계속 하던 문제를 수정했습니다.

* **Zendesk #17807**
Zendesk와 동일하게 비어 있는 광대한 영역을 통과할 수 #3103

* **Zendesk #17865**
PS4 및 XBox One의 폴백 논리
\
   Zendesk와 #3103

**버전 2.1.0.591**

* **Zendesk #3767**
PS4 광고 코드 조각, VMAP 리디렉션을 처리할 때 광고 해결이 실패합니다.
* **Zendesk #4096**
PS4 CSAI: 세그멘테이션 오류 광고 라이브러리가 VMAP 응답을 처리할 때 TVSDK에 세그멘테이션 오류가 발생할 때 발생하는 충돌을 해결했습니다.

* **Zendesk #4161**
무비 끝에 Trickplay 16x가 멈춥니다. Trickplay가 일반 재생으로 돌아갈 때 발생하는 교착 상태가 수정되었습니다.

* **Zendesk #4208**
닫힘 캡션이 켜져 있을 때 임의 충돌 닫힘 캡션이 활성화되어 있을 때 메모리 누수가 수정되었습니다.

* **Zendesk #4213**
PS4 CSAI: 모든 광고 관련 호출에 대한 기본 사용자-에이전트 문자열 변경

* **PTPLAY-7675** (내부) VMAP 또는 VAST 응답 내에서 호출할 때 트랜스코딩된 광고가 크리에이티브 재패키징을 재생하지 않았습니다. 광대한 광고가 있는 경우 자산에서 읽는 대신 광고에서 미디어 파일을 읽기만 하면 됩니다.

* **PTPLAY-7895** (내부) `allowMultipleAds=false`, no ads play 버그 수정 위치 `allowMultipleAds` 매개 변수를 올바르게 따르지 않았습니다.

* **PTPLAY-7896** (내부 광고가 XML 응답에 광고가 표시되는 순서로 표시되지 않는 PS4 수정 문제에 대해 순서대로 재생되지 않습니다.

* PS4 TVSDK는 게임 대신 미니 앱 내에서 재테스트되었습니다.

**버전 2.1.0.563**

* **Zendesk #3868**
TVSDK가 Playstation SDK 2.5를 지원합니까? TVSDK는 이제 2.5 Playstation SDK를 사용하여 빌드됩니다.

* **Zendesk #4093**
Pt Ads 요청의 targetingInfo 키-값 쌍.
\
   키/값 쌍을 구분하는 줄바꿈 문자가 추가되었습니다.

## 지원되는 기능 {#supported-features}

PlayStation 4용 TVSDK 2.1에서는 다음 기능이 지원됩니다.

**버전 2.1.0.621**

* 광고 대체, 광고 선택 로직의 데이지 체인(Zendesk #3103) 대체 규칙이 활성화된 VAST 광고(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형을 갖는 광고를 빈 광고로 취급하고 해당 위치에서 대체 광고를 사용하려고 합니다.대체 동작의 일부 측면을 구성할 수 있습니다

**버전 2.1.0.538**

* 재생, 일시 정지, 찾기를 포함한 HLS VOD 재생
* 적응형 비트율 스트리밍
* Primetime DRM 및 vanilla AES로 보호된 콘텐츠로 암호화된 컨텐츠 재생
* 기본 광고 동작 및 광고 용서를 사용하는 클라이언트 측 광고 삽입
* 크리에이티브 재포장
* WebVTT 자막
* 사용자 지정 시작 위치로 즉시 켜기
* 빠른 앞으로 및 빠른 되감기로 트릭 재생
* 302 리디렉션

## 유용한 리소스 {#helpful-resources}

* 에서 전체 도움말 설명서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지.
