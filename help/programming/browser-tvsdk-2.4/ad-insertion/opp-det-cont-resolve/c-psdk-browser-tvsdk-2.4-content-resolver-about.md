---
description: 브라우저 TVSDK는 타임라인에 광고를 배치하는 기본 영업 기회 생성기 및 콘텐츠 확인자를 제공하며 이러한 생성기 및 확인자는 매니페스트의 비표준 태그를 기반으로 합니다. 응용 프로그램에서 매니페스트에서 식별된 기회를 기반으로 타임라인을 변경해야 할 수 있습니다.
title: 기회 생성기 및 콘텐츠 해결자
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 기회 생성기 및 콘텐츠 해결자{#opportunity-generators-and-content-resolvers}

브라우저 TVSDK는 타임라인에 광고를 배치하는 기본 영업 기회 생성기 및 콘텐츠 확인자를 제공하며 이러한 생성기 및 확인자는 매니페스트의 비표준 태그를 기반으로 합니다. 응용 프로그램에서 매니페스트에서 식별된 기회를 기반으로 타임라인을 변경해야 할 수 있습니다.

An *`opportunity`* 일반적으로 광고 배치 기회를 나타내는 타임라인 내 관심 영역을 나타냅니다. 이 영업 기회는 타임라인에 영향을 줄 수 있는 사용자 지정 작업을 나타낼 수도 있습니다. An *`opportunity generator`* 타임라인에서 특정 기회(태그)를 식별하고 이러한 기회에 태그가 지정되었음을 TVSDK에 알립니다.

영업 기회는 의 타임라인에서 식별됩니다. `TimedMetata`. 다음 `ManifestCuesOpportunityGenerator` 다음을 기반으로 기회 생성 `TimedMetadata` 각 스플라이스 아웃 광고 태그에 대해 생성되는 개체(에서) `MediaPlayerItemConfig.adTags`) 매니페스트에서 감지되었습니다. 다음 `AdSignalingModeOpportunityGenerator` 다음을 기반으로 하는 초기 영업 기회 생성 `MediaPlayerItem` 및 연결된 광고 신호 모드를 입력합니다.

>[!TIP]
>
>다음과 같은 경우 `AdvertisingMetadata.livePreroll` 또는 `AdvertisingMetadata.preroll` 속성이 설정됨, `AdSignalingModeOpportunityGenerator` 라이브 스트림에 대한 프리롤 기회를 생성합니다.

애플리케이션에 기회(태그)에 대한 알림이 표시되면 애플리케이션은 예를 들어 일련의 광고를 삽입하여 타임라인을 변경할 수 있습니다. 기본적으로 브라우저 TVSDK는 적절한 *`content resolver`* 필요한 타임라인 변경 사항 또는 작업을 구현합니다. 응용 프로그램에서 기본 브라우저 TVSDK 광고 콘텐츠 확인자를 사용하거나 자체 콘텐츠 확인자를 등록할 수 있습니다.

다음을 사용할 수도 있습니다. `MediaPlayerItemConfig.adTags` 기본으로 더 많은 광고 마커 태그/큐를 추가하려면 `ManifestCuesOpportunityGenerator` 클래스 및 사용 `MediaPlayerItemConfig.subscribedTags` 따라서 TVSDK는 광고 워크플로 정보가 있을 수 있는 추가 태그에 대해 애플리케이션에 알릴 수 있습니다.

>[!TIP]
>
>의 기본값 `MediaPlayerItemConfig.adTags` 및 `MediaPlayerItemConfig.subscribeTags` 은(는) `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
