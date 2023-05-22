---
description: 비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.
title: VPAID 2.0 광고 지원
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# VPAID 2.0 광고 지원 {#vpaid-ad-support}

비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID) 2.0에서는 비디오 광고를 재생할 수 있는 공통 인터페이스를 제공합니다. 사용자에게 풍부한 미디어 경험을 제공하고 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양의 버전 2.0

   자세한 내용은 [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* 주문형 비디오(VOD) 콘텐츠가 포함된 선형 VPAID 광고
* 라이브 콘텐츠에서 브라우저 TVSDK는 프리롤 JavaScript VPAID 광고를 지원합니다.
* Flash 대체 모드에서 브라우저 TVSDK는 Flash 기반 VPAID 광고만 지원합니다.
* 선형 JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며, 광고 응답은 VPAID 광고의 미디어 유형을 다음으로 식별해야 합니다. `application/javascript`.

다음 기능은 지원되지 않습니다.

* VPAID 사양의 버전 1.0
* 스킵퍼블 광고
* 오버레이 광고, 동적 컴패니언 광고, 최소화 가능한 광고, 축소 가능한 광고 및 확장 가능한 광고와 같은 비선형 광고.
* VPAID 광고 미리 로드
* 라이브 콘텐츠의 VPAID 광고
* Flash VPAID 광고

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

다음 API 요소는 VPAID 2.0 광고를 지원합니다.

* 다음 `getCustomAdView` 방법 `MediaPlayer` 반환: `CustomAdView` object - VPAID 광고를 렌더링하는 웹 보기를 나타냅니다.

   에 대한 자세한 내용은 `getCustomAdView` 메서드, 참조 [MediaPlayer API 설명서](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` vpaid 로드 프로세스의 시간 제한을 설정합니다.

   기본 시간 초과 값은 10초입니다.

* API, `auditudeSettings.ignoreVPAIDAds`를 사용하면 Auditude 서버에서 받은 VPAID 광고를 무시할 수 있습니다. API가 Flash 폴백에 대해 작동하지 않습니다.

VPAID 광고가 재생되는 동안:

* VPAID 광고는 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭에 의존하는 코드는 작동하지 않습니다.
* 플레이어 인스턴스에서 일시 중지했다가 재생하고 VPAID 광고를 다시 시작하는 호출.
* VPAID 광고는 대화형일 수 있으므로 사전 정의된 기간이 없습니다.

   광고 서버 응답에 지정된 광고 기간 및 총 광고 브레이크 기간이 정확하지 않을 수 있습니다.
