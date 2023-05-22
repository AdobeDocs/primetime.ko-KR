---
description: 기회 생성기는 스트림의 사용자 지정 태그, 광고 시그널링 모드 사용자 지정 마커 등을 통해 배치 기회를 식별합니다. 기회 생성기는 이러한 배치 기회를 content resolver로 보내며, 이 resolver는 배치 기회의 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
title: 기회 생성기 및 콘텐츠 해결자 사용자 지정
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 개요 {#customize-opportunity-generators-and-content-resolvers-overview}

기회 생성기는 스트림의 사용자 지정 태그, 광고 시그널링 모드 사용자 지정 마커 등을 통해 배치 기회를 식별합니다. 기회 생성기는 이러한 배치 기회를 content resolver로 보내며, 이 resolver는 배치 기회의 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

TVSDK에는 다음과 같은 기본 영업 기회 생성기가 포함되어 있습니다.

* `ManifestCuesOpportunityGenerator` 기본 광고 큐에서 기회 생성( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` 지정된 광고 신호 모드에 대한 초기 기회를 생성합니다. 이는 모든 큐 또는 시간 초과된 메타데이터 정보를 무시합니다.
* `CustomMarkerOpportunityGenerator` 는 구워진 C3 광고를 대체할 수 있는 기회를 생성합니다.
* `AuditudeResolver`의 opportunity generator는 지연 광고 해결 이 설정되어 있으면 기회를 생성합니다.

TVSDK에는 기본 콘텐츠 해결자도 포함되어 있습니다.

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`: Primetime ad decisioning과 통신할 수 있습니다.

기본 기회 생성기 및 콘텐츠 해결자를 재정의하여 다음과 같은 방법으로 광고 워크플로를 사용자 정의할 수 있습니다.

* 광고 삽입에 대한 사용자 지정 태그를 인식합니다. 자세한 내용은 [기회 생성기 및 콘텐츠 해결자 사용자 지정](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* 사용자 지정된 광고 공급자를 만듭니다.
* 콘텐츠를 일시 중단합니다.
