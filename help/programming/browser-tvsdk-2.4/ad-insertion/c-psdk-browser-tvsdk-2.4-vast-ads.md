---
description: 브라우저 TVSDK가 주 광고 서버에 없는 광고를 요청할 때 플레이어는 보조 서버에서 광고를 요청해야 합니다. 비디오 광고 서비스 제공 템플릿(VAST)은 광고 서버와 비디오 플레이어 간의 통신 표준을 설정하며, 광고가 요청될 때 보조 광고 서버에서 보내는 응답입니다.
title: VAST 광고
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# VAST 광고 {#vast-ads}

브라우저 TVSDK가 주 광고 서버에 없는 광고를 요청할 때 플레이어는 보조 서버에서 광고를 요청해야 합니다. 비디오 광고 서비스 제공 템플릿(VAST)은 광고 서버와 비디오 플레이어 간의 통신 표준을 설정하며, 광고가 요청될 때 보조 광고 서버에서 보내는 응답입니다.

VAST에 대한 자세한 내용은 [디지털 비디오 광고 서비스 제공 템플릿(VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

브라우저 TVSDK는 다음 VAST 광고 요소를 지원합니다.

## 래퍼 및 인라인 광고 {#section_11B8A1A8F52F4F77981C6AAC02185087}

지원되는 요소는 다음과 같습니다.

* **`wrapper`** 플레이어가 광고를 요청하기 위해 보조 광고 서버에 문의해야 하는 경우 래퍼 요소가 리디렉션 정보를 제공합니다. 하나의 래퍼 요소는 궁극적으로 VAST 광고를 가리키는 여러 래퍼를 가리킬 수 있습니다.

* **`inline`** 지원되는 필수 요소는 다음과 같습니다.

* `AdSystem`
* `AdTitle`
* `Impression`

  지원되는 선택적 요소는 다음과 같습니다.

* `Description`
* `Survey`
* `Error`

## 광고 {#section_0121F948CB074E49A8132D202786CAA4}

이 요소는 VAST 광고의 일부이며 `creative` 선형 광고, 비선형 광고 또는 컴패니언 광고를 지원할 수 있는 요소입니다. 다음에서 `creative` 요소, `id`, `sequence`, 및 `adId` 요소가 지원됩니다.

다음은 광고 유형에 대한 자세한 정보입니다.

* **선형 광고** 지원되는 요소는 다음과 같습니다.

   * `TrackingEvent`, 다음을 포함 `Tracking` 요소를 생성하지 않습니다.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, 다음 포함:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

        >[!TIP]
        >
        >이 요소에서 `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`, 및 `type` 속성이 지원됩니다.

* **비선형 광고** 지원되는 요소는 다음과 같습니다.

   * `Non-linear`

     >[!TIP]
     >
     >이 요소에서 `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`, 및 `minSuggestedDuration` 속성이 지원됩니다.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **컴패니언 광고** 지원되는 요소는 다음과 같습니다.

   * `Companion`

     >[!TIP]
     >
     >이 요소에서 `id`, `width`, `height`, `apiFramework`, `expandedWidth`, 및 `expandedHeight` 속성이 지원됩니다.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 확장 {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Auditude 전용 확장만 지원됩니다.

* `Extension`
