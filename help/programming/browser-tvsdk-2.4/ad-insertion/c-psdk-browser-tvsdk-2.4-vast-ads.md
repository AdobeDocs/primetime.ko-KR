---
description: 브라우저 TVSDK가 기본 광고 서버에 없는 광고를 요청하는 경우 플레이어는 보조 서버에서 광고를 요청해야 합니다. VAST 파섹(비디오 광고 서비스 템플릿)는 광고 서버와 비디오 플레이어 간의 통신 표준을 설정하며 광고가 요청될 때 보조 광고 서버에서 보내는 응답입니다.
seo-description: 브라우저 TVSDK가 기본 광고 서버에 없는 광고를 요청하는 경우 플레이어는 보조 서버에서 광고를 요청해야 합니다. VAST 파섹(비디오 광고 서비스 템플릿)는 광고 서버와 비디오 플레이어 간의 통신 표준을 설정하며 광고가 요청될 때 보조 광고 서버에서 보내는 응답입니다.
seo-title: 광대한 광고
title: 광대한 광고
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 광대한 광고 {#vast-ads}

브라우저 TVSDK가 기본 광고 서버에 없는 광고를 요청하는 경우 플레이어는 보조 서버에서 광고를 요청해야 합니다. VAST 파섹(비디오 광고 서비스 템플릿)는 광고 서버와 비디오 플레이어 간의 통신 표준을 설정하며 광고가 요청될 때 보조 광고 서버에서 보내는 응답입니다.

VAST에 대한 자세한 내용은 VAST 파섹 [디지털 비디오 광고 서비스 템플릿(VAST 파섹) 3.0을 참조하십시오](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

Browser TVSDK는 다음과 같은 VAST 광고 요소를 지원합니다.

## 래퍼 및 인라인 광고 {#section_11B8A1A8F52F4F77981C6AAC02185087}

다음 요소가 지원됩니다.

* **`wrapper`** 플레이어에서 광고를 요청하기 위해 보조 광고 서버에 문의해야 하는 경우 래퍼 요소는 리디렉션 정보를 제공합니다. 하나의 래퍼 요소는 VAST 광고를 가리키는 여러 래퍼를 가리킬 수 있습니다.

* **`inline`** 다음과 같은 필수 요소가 지원됩니다.

* `AdSystem`
* `AdTitle`
* `Impression`

   다음과 같은 선택적 요소가 지원됩니다.

* `Description`
* `Survey`
* `Error`

## 크리에이티브 {#section_0121F948CB074E49A8132D202786CAA4}

이 요소는 VAST 광고의 일부인 파일이며 선형 광고, 비선형 광고 또는 컴패니언 광고를 지원할 수 있는 `creative` 요소를 포함합니다. 요소에서 `creative``id`요소, `sequence`요소 `adId` 및 요소가 지원됩니다.

다음은 광고 유형에 대한 자세한 정보입니다.

* **선형 광고** 다음 요소가 지원됩니다.

   * `TrackingEvent`에 `Tracking` 있는 값을 찾습니다.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, including following:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`
         [!TIP]
이 요소에서는 `id`, `bitrate`, `delivery``width`, `height`Subsequence, Subsequence `scalable`및 Attributes가 `maintainAspectRatio``apiFramework``type` 지원됩니다.

* **비선형 광고** 다음 요소가 지원됩니다.

   * `Non-linear`
      [!TIP]
이 요소에서는 `id`, `width`, `height``apiFramework`, `expandedWidth`Subsequence, Subsequence `expandedHeight`및 Attributes가 `scalable``maintainAspectRatio``minSuggestedDuration` 지원됩니다.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **함께 사용 가능한 광고** 다음 요소가 지원됩니다.

   * `Companion`
      [!TIP]
이 요소에서는 `id`, `width`, `height``apiFramework`, `expandedWidth``expandedHeight` ,및속성이 지원됩니다.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 익스텐션 {#section_17401C75F419453BAE83637EEB6E1E60}

[!TIP]
Auditude 관련 익스텐션만 지원됩니다.

* `Extension`