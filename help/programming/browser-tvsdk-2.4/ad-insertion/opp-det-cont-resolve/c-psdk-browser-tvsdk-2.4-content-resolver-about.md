---
description: Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기 및 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에서 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.
seo-description: Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기 및 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에서 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.
seo-title: 기회 생성기 및 컨텐츠 해결
title: 기회 생성기 및 컨텐츠 해결
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# 기회 생성기 및 컨텐츠 해상도{#opportunity-generators-and-content-resolvers}

Browser TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기 및 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 매니페스트에서 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.

*`opportunity`*&#x200B;은 일반적으로 광고 배치 기회를 나타내는 타임라인의 관심 영역을 나타냅니다. 이 기회는 타임라인에 영향을 줄 수 있는 사용자 지정 작업을 나타낼 수도 있습니다. *`opportunity generator`*&#x200B;은 타임라인에서 특정 기회(태그)를 식별하고 TVSDK에 이러한 기회들에 태그가 지정되었음을 알립니다.

기회는 `TimedMetata`의 타임라인에서 식별됩니다. `ManifestCuesOpportunityGenerator`은 매니페스트에서 검색된 각 스플라인 아웃 광고 태그(`MediaPlayerItemConfig.adTags`에서)에 대해 만들어진 `TimedMetadata` 개체를 기반으로 기회를 만듭니다. `AdSignalingModeOpportunityGenerator`은 `MediaPlayerItem` 유형 및 관련 광고 신호 모드를 기반으로 하는 초기 기회를 만듭니다.

>[!TIP]
>
>`AdvertisingMetadata.livePreroll` 또는 `AdvertisingMetadata.preroll` 속성이 설정된 경우 `AdSignalingModeOpportunityGenerator`은 실시간 스트림에 대한 프리롤 기회를 생성합니다.

애플리케이션에 기회(태그)에 대한 알림을 받으면 애플리케이션이 예를 들어 일련의 광고를 삽입하여 타임라인을 변경할 수 있습니다. 기본적으로 브라우저 TVSDK는 필요한 타임라인 변경 사항 또는 작업을 구현하기 위해 적절한 *`content resolver`*&#x200B;을 호출합니다. 응용 프로그램은 기본 Browser TVSDK 광고 내용 확인자를 사용하거나 자체 컨텐츠 확인자를 등록할 수 있습니다.

또한 `MediaPlayerItemConfig.adTags`을(를) 사용하여 기본 `ManifestCuesOpportunityGenerator` 클래스에 대한 광고 마커 태그/큐를 추가하고 `MediaPlayerItemConfig.subscribedTags`를 사용하여 TVSDK가 광고 워크플로우 정보가 있을 수 있는 추가 태그에 대해 응용 프로그램에 통지할 수 있습니다.

>[!TIP]
>
>`MediaPlayerItemConfig.adTags` 및 `MediaPlayerItemConfig.subscribeTags`의 기본값은 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`입니다.

