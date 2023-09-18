---
title: TVSDK 2.1 PlayStation 4 릴리스 노트
description: PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제에 대해 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# TVSDK 2.1 PlayStation 4 릴리스 노트 {#tvsdk-playstation-release-notes}

PlayStation 4용 TVSDK 2.1 릴리스 정보에서는 TVSDK 2.1 PlayStation 4의 지원되는 기능과 알려진 문제에 대해 설명합니다.

## 해결된 문제 {#resolved-issues}

다음은 PlayStation 4용 TVSDK 2.1에 대해 해결된 문제입니다.

**버전 2.1.0.638**

* **PTPLAY-10439:**
VMAP 래퍼 광고 링크가 끊겼을 때 플레이어가 준비 중 상태로 멈추고 있었습니다(전송 중이 아님). `onComplete` (호출자에게).

* **PTPLAY-10179:**
  `creativeRepackaging` 및 `fallbackOnInvalidCreative` 이제 값이 기본적으로 꺼져 있습니다. 또한 `creativeRepackaging` 플래그가 설정되었지만 설정되지 않음 `creativeRepackaging` 형식을 입력했습니다. `onRepackagingComplete` 광고 브레이크에 광고가 있는 횟수만큼 가 호출되어 광고 브레이크가 여러 번 생성됩니다.

* **Zendesk #10304**: ad forveness on/off 변수가 초기화되지 않았습니다. 이제에서 변수를 초기화합니다. `DataSetEntry's` 토르

* **PTPLAY-10318:**
백그라운드 모드에 대한 지원이 도입되었습니다.
* **Zendesk # 17409:**
트릭 재생 모드로 들어갔다가 일반 재생 모드로 돌아간 다음 다시 트릭 재생 모드로 전환될 때 재생 위치는 점프되었습니다.
* **PTPLAY-9552:**
응답 XML 파일을 구문 분석한 후, 이제 광고가 존재하지 않을 때마다 오류 코드(1108)가 핑된다.
* **PTPLAY-9551:**
Auditude 처리 후 광고 브레이크가 없으면 CRS가 호출됩니다 **onPrefetchComplete** groupCount가 감소합니다. 광고 브레이크가 없기 때문에 **groupCount** 는 0이고 1씩 감소합니다. 이전 **groupCount** 다음과 같음 **uint32_t** 때문에 최대값으로 변경되던 작업을 중단했습니다. 현재 **int32_t**.

**버전 2.1.0.621**

* **Zendesk #4555**
메모리 문제 발생 시 즉시 로딩 오류 발생 - `MediaItemLoader` 릴리스 중 충돌 발생 시 수정 `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: 일부 광고 추적 URL이 실행되지 않음
   * 인라인 광고를 가리키는 일부 VAST 광고에는 추적 URL이 누락되었습니다.
   * VAST XML의 광고에 노출 태그가 여러 개 있는 경우 첫 노출 URL만 저장되고 나머지는 무시됩니다. 이제 모든 노출 URL이 저장되고 나중에 ping됩니다.
* **Zendesk #17224**
PS4 사용자 에이전트가 primetime 정보를 UAString의 끝으로 이동
* **Zendesk #17226**
2.x CSAI: 일부 광고만 결합됩니다.\
  insertBy 또는 eraseBy 작업으로 인해 타임라인이 변경되었음을 표시하고 그에 따라 기간 전환을 수행합니다.

* **Zendesk #17284**
  [모든 플랫폼] 폐쇄 캡션이 표시되지 않습니다.\
  HLS - 지원 `EXT-X-MEDIA-TIME` VTT 캡션 파일에 대한 태그입니다.

* **Zendesk #17889**
PS4에서 &quot;Milky&quot; 재생\
  적용된 올바른 yoffset(색상 변환용)

* **Zendesk #17954**
광고 대체 논리 + 빈 vast 처리\
  Vast 래퍼 중 하나가 비어 있는 경우 Vast 파서가 래퍼를 계속 처리하는 데 사용하는 문제를 해결했습니다.

* **Zendesk #17807**
빈 vast를 지나갈 수 없음 Zendesk #3103과 같음

* **Zendesk #17865**
PS4 및 XBox One의 폴백 논리\
  Zendesk #3103과 동일

**버전 2.1.0.591**

* **Zendesk #3767**
PS4 광고 코드 스니펫을 사용하면 VMAP 리디렉션을 처리할 때 광고 해결이 실패합니다.
* **Zendesk #4096**
PS4 CSAI: 세그멘테이션 오류 광고 라이브러리에서 VMAP 응답을 처리할 때 TVSDK에서 세그멘테이션 오류가 발생하는 경우 충돌이 수정되었습니다.

* **Zendesk #4161**
트릭플레이가 정상 재생으로 돌아올 때 발생하는 교착 상태를 수정했습니다.

* **Zendesk #4208**
폐쇄 캡션이 켜져 있을 때 무작위 충돌 폐쇄 캡션이 활성화되면 고정 메모리 누수

* **Zendesk #4213**
PS4 CSAI: 모든 광고 관련 호출에 대한 기본 사용자 에이전트 문자열 변경 사용자 에이전트 문자열은 브라우저에서 + Primetime 문자열을 사용하는 것과 동일한 UA 문자열을 사용하여 만들어집니다

* **PTPLAY-** (내부) VMAP 또는 VAST 응답 내에서 호출될 때 Creative Repackaging이 실패하여 트랜스코딩된 광고가 재생되지 않습니다. 수정 사항은 방대한 광고의 경우 에셋에서 읽는 대신 광고에서 미디어 파일을 읽는 것입니다.

* **PTPLAY-** (내부) 다음의 경우 `allowMultipleAds=false`, 광고 재생 없음 버그 수정 위치 `allowMultipleAds` 매개 변수가 올바르게 팔로우되지 않았습니다.

* **PTPLAY-** (내부) 광고가 PS4에서 시퀀스 순서를 벗어나서 재생됨 광고가 XML 응답에 표시된 순서로 표시되지 않던 문제가 해결되었습니다.

* PS4 TVSDK는 게임 대신 미니 앱 내에서 다시 테스트되었습니다.

**버전 2.1.0.563**

* **Zendesk #3868**
TVSDK가 Playstation SDK 2.5를 지원합니까? TVSDK는 이제 2.5 Playstation SDK로 빌드되었습니다.

* **Zendesk #4093**
Pt Ads 요청의 targetingInfo 키-값 쌍.\
  키/값 쌍을 구분하는 줄바꿈 문자가 추가되었습니다.

## 지원되는 기능 {#supported-features}

PlayStation 4용 TVSDK 2.1에서는 다음 기능이 지원됩니다.

**버전 2.1.0.621**

* 광고 폴백, 광고 선택 논리의 데이지 체인(Zendesk #3103) 폴백 규칙이 활성화된 VAST 광고(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용하려고 시도합니다. 폴백 동작의 몇 가지 측면을 구성할 수 있습니다

**버전 2.1.0.538**

* 재생, 일시 중지, 찾기를 포함한 HLS VOD 재생
* 적응형 비트율 스트리밍
* Primetime DRM 및 바닐라 AES 보호 콘텐츠로 암호화된 콘텐츠 재생
* 기본 광고 동작 및 광고 용서가 있는 클라이언트측 광고 삽입
* 크리에이티브 리패키징
* WebVTT 폐쇄 캡션
* 사용자 정의 시작 위치로 즉시 켜기
* 빠른 전진 및 빠른 되감기로 트릭 플레이
* 302 리디렉션

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://experienceleague.adobe.com/docs/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
