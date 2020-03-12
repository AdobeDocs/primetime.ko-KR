---
description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 리치 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-description: 비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 리치 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-title: VPAID 2.0 광고 지원
title: VPAID 2.0 광고 지원
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VPAID 2.0 광고 지원 {#vpaid-ad-support}

비디오 플레이어(VPAID) 2.0은 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. 사용자에게 리치 미디어 경험을 제공하고 발행자는 광고를 보다 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.

지원되는 기능은 다음과 같습니다.

* VPAID 사양 버전 2.0

   자세한 내용은 IAB VPAID [2.0을 참조하십시오](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* VOD(Video-On-Demand) 컨텐츠가 포함된 선형 VPAID 광고
* 라이브 컨텐츠에서 브라우저 TVSDK는 프리롤 JavaScript VPAID 광고를 지원합니다.
* Flash 폴백 모드에서 브라우저 TVSDK는 Flash 기반 VPAID 광고만 지원합니다.
* 선형 JavaScript VPAID 광고

   VPAID 광고는 JavaScript 기반이어야 하며 광고 응답으로 VPAID 광고의 미디어 유형을 `application/javascript`식별해야 합니다.

다음 기능은 지원되지 않습니다.

* VPAID 사양 버전 1.0
* 확장 가능한 광고
* 오버레이 광고, 동적 컴패니언 광고, 최소화 가능한 광고, 축소 가능한 광고, 확장 가능한 광고와 같은 비선형 광고.
* VPAID 광고 사전 로드
* 라이브 콘텐츠의 유료 광고
* Flash VPAID 광고

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

다음 API 요소는 VPAID 2.0 광고를 지원합니다.

* VPAID 광고를 렌더링하는 웹 보기를 나타내는 `getCustomAdView` 개체를 반환하는 `MediaPlayer` `CustomAdView` 방법입니다.

   이 `getCustomAdView` 방법에 대한 자세한 내용은 MediaPlayer [API 설명서를](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)참조하십시오.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` vpaid 로드 프로세스의 시간 초과를 설정합니다.

   기본 시간 초과 값은 10초입니다.

* API를 `auditudeSettings.ignoreVPAIDAds`사용하면 Auditude 서버로부터 받은 VPAID 광고를 무시할 수 있습니다. Flash Fallback에서는 API가 작동하지 않습니다.

VPAID 광고가 재생되는 동안:

* VPAID 광고는 플레이어 보기 위의 보기 컨테이너에 표시되므로 플레이어 보기에서 사용자의 탭 사용에 의존하는 코드가 작동하지 않습니다.
* 플레이어 인스턴스에서 일시 중지 및 재생 호출이 일시 중지되고 VPAID 광고를 다시 시작합니다.
* 광고는 인터랙티브한 광고이므로 VPAID 광고의 지속 시간은 사전 정의되어 있지 않습니다.

   광고 서버 응답에 지정된 광고 지속 시간과 총 광고 중단 기간이 정확하지 않을 수 있습니다.