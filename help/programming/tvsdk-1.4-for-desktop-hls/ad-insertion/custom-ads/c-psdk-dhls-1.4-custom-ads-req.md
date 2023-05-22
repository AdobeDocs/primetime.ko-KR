---
description: 비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID)는 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. VPAID는 사용자에게 풍부한 미디어 경험을 제공하며 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.
title: 사용자 지정 광고 요구 사항
exl-id: c13748d6-23f1-4f34-95b4-7b532db6e536
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 사용자 지정 광고 요구 사항 {#custom-ad-requirements}

TVSDK 플레이어는 디지털 비디오 플레이어 VPAID(Ad-Interface Definition) 광고를 재생하고 광고 로드 상태를 표시할 수 있습니다. 광고에 오류가 있거나 광고를 로드하는 데 너무 오래 걸리는 경우 TVSDK는 이러한 광고를 무시합니다.

비디오 플레이어 광고 서비스 제공 인터페이스 정의(VPAID)는 비디오 광고를 재생하는 공통 인터페이스를 제공합니다. VPAID는 사용자에게 풍부한 미디어 경험을 제공하며 게시자가 광고를 더 잘 타겟팅하고, 광고 노출 횟수를 추적하고, 비디오 콘텐츠를 수익화할 수 있도록 합니다.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK는 다음 기능을 지원합니다.

* VPAID 사양의 버전 1.0 및 2.0
* 선형 VPAID 광고 온디맨드(VOD) 콘텐츠
* Flash VPAID 광고

   VPAID 광고는 Flash 기반이어야 하며, 광고 응답은 VPAID 광고의 미디어 유형을 다음으로 식별해야 합니다. `application/x-shockwave-flash`.

다음 기능은 지원되지 않습니다.

* 오버레이 광고 및 동적 컴패니언 광고와 같은 비선형 광고
* VPAID 광고 미리 로드
* 라이브 콘텐츠의 VPAID 광고
* JavaScript VPAID 광고

## 상태 로드 중 {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK는 다음 이벤트를 전달합니다.

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

다음 이후 `AdStopped` 이벤트이면 TVSDK가 비디오 콘텐츠를 다시 시작합니다.

>[!TIP]
>
>값을 0으로 지정하면 TVSDK는 광고가 로드되거나 오류가 발생할 때까지 광고를 로드하려고 합니다.

## 광고 무시 {#section_3EA452F420884335AE90DF23C17E416A}

광고를 로드하는 데 너무 오래 걸리거나 광고에 오류가 있는 경우 TVSDK가 광고를 무시할 수 있고 광고 Pod의 다음 광고가 자동으로 재생됩니다.

다음과 같은 경우 `AuditudeSettings.customAdLoadTimeout` 이 설정은 0보다 큰 시간(초)을 지정합니다. tvsdk는 지정된 기간으로 광고를 로드하려고 합니다. 광고를 로드할 수 없는 경우 광고를 건너뜁니다. 예를 들어 을 구성하는 경우 `AuditudeSettings.customAdLoadTimeout:5`, TVSDK는 최대 5초 동안 광고 로드를 시도합니다. 광고가 여전히 로드되지 않으면 무시됩니다.
