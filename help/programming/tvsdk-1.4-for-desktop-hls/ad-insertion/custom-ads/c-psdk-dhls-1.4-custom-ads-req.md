---
description: VPAID(Video Player Ad-Serving Interface Definition)는 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. VPAID는 사용자를 위한 리치 미디어 경험을 제공하고 발행자는 광고를 더 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-description: VPAID(Video Player Ad-Serving Interface Definition)는 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. VPAID는 사용자를 위한 리치 미디어 경험을 제공하고 발행자는 광고를 더 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.
seo-title: 맞춤형 광고 요구 사항
title: 맞춤형 광고 요구 사항
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 맞춤형 광고 요구 사항 {#custom-ad-requirements}

TVSDK 플레이어는 VPAID(Digital Video Player Ad-Interface Definition) 광고를 재생하고 광고 로드 상태를 표시할 수 있습니다. 광고에 오류가 있거나 광고를 로드하는 데 시간이 너무 오래 걸리는 경우 TVSDK는 이러한 광고를 무시합니다.

VPAID(Video Player Ad-Serving Interface Definition)는 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. VPAID는 사용자를 위한 리치 미디어 경험을 제공하고 발행자는 광고를 더 효과적으로 타겟팅하고 광고 노출 횟수를 추적하며 비디오 컨텐츠를 상용화할 수 있습니다.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK는 다음 기능을 지원합니다.

* VPAID 사양 버전 1.0 및 2.0
* VOD(Video-On-Demand) 컨텐츠의 선형 VPAID 광고
* Flash VPAID 광고

   VPAID 광고는 Flash 기반이어야 하며 광고 응답으로 VPAID 광고의 미디어 유형을 `application/x-shockwave-flash`식별해야 합니다.

다음 기능은 지원되지 않습니다.

* 오버레이 광고 및 동적 컴패니언 광고와 같은 비선형 광고
* VPAID 광고 사전 로드
* 라이브 콘텐츠의 유료 광고
* JavaScript VPAID 광고

## 로드 상태 {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK는 다음 이벤트를 전달합니다.

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

이벤트 `AdStopped` 후 TVSDK는 비디오 컨텐츠를 다시 시작합니다.

>[!TIP]
>
>값을 0으로 지정하면 TVSDK가 로드되거나 오류가 발생할 때까지 광고를 로드합니다.

## 광고 무시 {#section_3EA452F420884335AE90DF23C17E416A}

광고를 로드하는 데 시간이 너무 오래 걸리거나 광고에 오류가 있는 경우 TVSDK가 광고를 무시할 수 있으며 광고 창의 다음 광고가 자동으로 재생됩니다.

이 `AuditudeSettings.customAdLoadTimeout` 설정이 0보다 큰 시간(초)을 지정하는 경우 TVSDK는 지정된 지속 시간으로 광고를 로드합니다. 광고를 로드할 수 없으면 광고를 건너뜁니다. 예를 들어, 구성하는 경우 TVSDK `AuditudeSettings.customAdLoadTimeout:5`는 최대 5초 동안 광고를 로드합니다. 광고가 로드되지 않으면 무시됩니다.
