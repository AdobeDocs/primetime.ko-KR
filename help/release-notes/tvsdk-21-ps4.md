---
title: TVSDK 2.1 PlayStation 4 릴리스 노트
seo-title: TVSDK 2.1 PlayStation 4 릴리스 노트
description: PlayStation 4용 TVSDK 2.1 릴리스 노트는 TVSDK 2.1 PlayStation 4에서 지원되는 기능과 알려진 문제를 설명합니다.
seo-description: PlayStation 4용 TVSDK 2.1 릴리스 노트는 TVSDK 2.1 PlayStation 4에서 지원되는 기능과 알려진 문제를 설명합니다.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# TVSDK 2.1 PlayStation 4 릴리스 노트 {#tvsdk-playstation-release-notes}

PlayStation 4용 TVSDK 2.1 릴리스 노트는 TVSDK 2.1 PlayStation 4에서 지원되는 기능과 알려진 문제를 설명합니다.

## 해결된 문제 {#resolved-issues}

다음은 PlayStation 4용 TVSDK 2.1의 해결된 문제입니다.

**버전 2.1.0.638**

* **PTPLAY-10439:** VMAP 래퍼 광고 링크가 끊기면 플레이어가 준비 상태에 갇히게 됩니다(호출자에게 전송되지 않음). `onComplete`

* **PTPLAY-10179:**
   `creativeRepackaging` 및 `fallbackOnInvalidCreative` 값은 이제 기본적으로 꺼져 있습니다. 또한 플래그가 설정되었지만 `creativeRepackaging` 형식이 제공되지 않은 `creativeRepackaging` `onRepackagingComplete` 경우 광고 브레이크에 광고가 있는 횟수만큼 호출되어 광고 나누기가 여러 번 생성되었습니다.

* **Zendesk #10304**:광고 형식/해제 변수가 초기화되지 않았습니다. 이제 `DataSetEntry's` Tor에서 변수를 초기화합니다.

* **PTPLAY-10318:**&#x200B;배경 모드에 대한 지원이 도입되었습니다.
* **Zendesk 번호 17409:**&#x200B;트릭 재생 모드로 전환한 다음 다시 일반 재생 모드로 전환한 다음 다시 트릭 재생 모드로 전환하면 재생 위치가 이동되었습니다.
* **PTPLAY-9552:**&#x200B;응답 XML 파일을 구문 분석한 후 광고가 없을 때마다 오류 코드 1108이 ping됩니다.
* **PTPLAY-9551:** Auditude 처리 후 광고 브레이크가 없으면 CRS가 **onPrefetchComplete를** 호출하여 groupCount를 감소시킵니다. 광고 브레이크가 없으므로 groupCount **는** 0이고 1씩 감소합니다. 이전에는 **groupCount** 가 **uint32_t** 로 변경되었기 때문에 최대 값으로 변경되었습니다. 이제 **int32_t입니다**.

**버전 2.1.0.621**

* **Zendesk #4555** Instant on Memory issues leading-Loading errors - `MediaItemLoader` Remoting for crash while release `mediaitemloader`

* **Zendesk #17223** 2.x CSAI:일부 광고 추적 URL이 실행되지 않음
   * 인라인 광고를 가리키던 일부 VAST 광고가 추적 URL을 누락했습니다.
   * VAST XML에 광고에 노출 태그가 여러 개 있을 때 첫 번째 노출 URL만 저장되고 나머지는 무시됩니다. 이제 모든 노출 URL이 저장되고 나중에 핑됩니다.
* **Zendesk #17224** PS4 사용자 에이전트, Primetime 정보를 UAString 끝으로 이동
* **Zendesk #17226** 2.x CSAI:일부 광고는 이에 포함되지 않았습니다.\
   insertBy 또는 eraseBy 작업으로 인해 타임라인이 변경되었음을 알리고 이에 따라 기간 전환을 수행하는 수정입니다.

* **Zendesk #17284**
   [모든 플랫폼] 자막이 표시되지 않습니다.\
   HLS - VTT 캡션 파일에 대한 `EXT-X-MEDIA-TIME` 태그를 지원합니다.

* **Zendesk #17889** PS4의 Playback &quot;Milky&quot;\
   올바른 설정 적용(색상 변환용)

* **Zendesk #17954**&#x200B;광고 폴백 로직 + 빈 광대한 처리\
   Vast 래퍼 중 하나가 비어 있는 경우 Vast 구문 분석기가 래퍼를 계속 처리하는 데 사용되던 문제를 수정했습니다.

* **Zendesk #17807**&#x200B;빈 광석을 넘을 수 없습니다Zendesk #3103과 동일

* **Zendesk #17865** PS4 및 XBox One의 폴백 로직\
   Zendesk #3103과 동일

**버전 2.1.0.591**

* **Zendesk #3767** PS4 광고 코드 조각, VMAP 리디렉션을 처리할 때 광고 해결에 실패합니다.
* **Zendesk #4096** PS4 CSAI:세그멘테이션 오류 광고 라이브러리가 VMAP 응답을 처리할 때 TVSDK에서 세그멘테이션 오류를 발생시키는 경우 발생하는 충돌을 수정했습니다.

* **Zendesk #4161**&#x200B;동영상 멈춤이 끝날 때 16xTrickplay트릭플레이가 정상적인 재생으로 돌아갈 때 발생하는 교착 상태가 수정되었습니다.

* **Zendesk #4208**&#x200B;자막이 켜진 경우 임의 충돌자막이 활성화되면 메모리 누수가 해결됨

* **Zendesk #4213** PS4 CSAI:모든 광고 관련 호출에 대한 기본 사용자-에이전트 문자열 변경사용자-에이전트 문자열은 브라우저가 + Primetime 문자열 추가를 사용하는 것과 동일한 UA 문자열을 사용하여 만듭니다

* **PTPLAY-7675** (내부)트랜스코딩된 광고가 재생되지 않습니다. VMAP 또는 VAST 응답 내에서 Creative Repackaging을 호출할 때 실패했습니다. 다양한 광고의 경우 자산에서 읽는 대신 광고에서 미디어를 읽는 것이 수정되었습니다.

* **PTPLAY-7895** (내부) `allowMultipleAds=false`인 경우, 광고 재생매개 변수가 올바르게 표시되지 않는 `allowMultipleAds` 버그가 없습니다.

* **PTPLAY-7896** (내부)PS4에서 광고가 XML 응답에 표시된 순서대로 표시되지 않는 문제가 수정되었습니다.

* PS4 TVSDK는 게임이 아닌 미니 앱에서 다시 테스트되었습니다.

**버전 2.1.0.563**

* **Zendesk #3868** TVSDK가 Playstation SDK 2.5를 지원합니까? TVSDK는 현재 2.5 Playstation SDK로 빌드됩니다.

* **Zendesk #4093**&#x200B;타깃팅Pt 광고 요청의 정보 키-값 쌍.\
   키/값 쌍을 분리하는 줄바꿈 문자가 추가되었습니다.

## 지원되는 기능 {#supported-features}

PlayStation 4용 TVSDK 2.1에서 지원되는 기능은 다음과 같습니다.

**버전 2.1.0.621**

* 광고 폴백, 광고 선택 로직 데이지 체인(Zendesk #3103)폴백 규칙이 활성화된 VAST 파섹(크리에이티브)의 경우 TVSDK는 잘못된 MIME 유형의 광고를 빈 광고로 취급하고 대신 폴백 광고를 사용합니다.폴백 동작의 일부 측면을 구성할 수 있습니다

**버전 2.1.0.538**

* 재생, 일시 정지, 검색 등 HLS VOD 재생
* 적응형 비트 전송률 스트리밍
* Primetime DRM 및 바닐라 AES로 보호된 콘텐츠를 통해 암호화된 컨텐츠 재생
* 기본 광고 비헤이비어와 광고 용서를 위한 클라이언트측 광고 삽입
* 크리에이티브 재패키징
* WebVTT 자막
* 사용자 정의 시작 위치로 즉시 설정
* 빨리 감기 및 빠른 되감기로 재생
* 302 리디렉션

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.