---
description: Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기와 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.
seo-description: Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기와 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.
seo-title: 기회 생성기 및 컨텐츠 해결
title: 기회 생성기 및 컨텐츠 해결
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 기회 생성기 및 컨텐츠 해결{#opportunity-generators-and-content-resolvers}

Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기와 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.

일반적으로 광고 배치 기회를 나타내는 타임라인의 관심 영역을 *`opportunity`* 나타냅니다. 이 기회에 타임라인에 영향을 줄 수 있는 사용자 지정 작업을 표시할 수도 있습니다. 타임라인에서 특정 기회(태그)를 *`opportunity generator`* 식별하고 이러한 기회에 대해 TVSDK에 알립니다.

의 타임라인에서 기회가 식별됩니다 `TimedMetata`. 이렇게 `ManifestCuesOpportunityGenerator` 하면 매니페스트에서 검색된 각 스플라이스 아웃 광고 태그(in)에 대해 만들어진 `TimedMetadata` 객체를 기반으로 기회가 `MediaPlayerItemConfig.adTags`만들어집니다. The `AdSignalingModeOpportunityGenerator` creates the initial opportunity that is based on the `MediaPlayerItem` type and its associated ad signing mode.

>[!TIP]
>
>또는 속성이 `AdvertisingMetadata.livePreroll` 설정된 경우 실시간 스트림에 대한 프리롤 기회를 `AdvertisingMetadata.preroll` `AdSignalingModeOpportunityGenerator` 생성합니다.

애플리케이션에 기회(태그)에 대한 알림을 받으면 애플리케이션에서 일련의 광고를 삽입하는 등 타임라인을 변경할 수 있습니다. 기본적으로 브라우저 TV SDK는 필요한 타임라인 변경 사항 또는 작업을 *`content resolver`* 구현하는 데 적절한 호출을 호출합니다. 응용 프로그램은 기본 Browser TVSDK 광고 컨텐츠 확인자를 사용하거나 자체 컨텐츠 확인자를 등록할 수 있습니다.

를 사용하여 기본 `MediaPlayerItemConfig.adTags` 클래스에 대한 광고 마커 태그/큐를 더 추가하고 `ManifestCuesOpportunityGenerator` `MediaPlayerItemConfig.subscribedTags` TVSDK가 광고 워크플로우 정보가 있을 수 있는 추가 태그에 대해 응용 프로그램에 알릴 수 있도록 할 수도 있습니다.

>[!TIP]
>
>의 `MediaPlayerItemConfig.adTags` 기본값은 `MediaPlayerItemConfig.subscribeTags` 입니다 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

