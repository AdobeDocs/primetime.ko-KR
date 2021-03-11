---
description: 기회 생성기는 스트림의 사용자 정의 태그, 신호 모드 사용자 정의 마커 등을 사용하여 배치 기회를 식별합니다. 기회 생성기는 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램에 이러한 배치 기회를 보냅니다.
title: 기회 생성기 및 컨텐츠 해상도 사용자 정의
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# 개요 {#customize-opportunity-generators-and-content-resolvers-overview}

기회 생성기는 스트림의 사용자 정의 태그, 신호 모드 사용자 정의 마커 등을 사용하여 배치 기회를 식별합니다. 기회 생성기는 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램에 이러한 배치 기회를 보냅니다.

TVSDK에는 다음과 같은 기본 기회 생성기가 포함되어 있습니다.

* `ManifestCuesOpportunityGenerator` 기본 광고 큐에서 기회()를  `#EXT-X-CUE`생성합니다.

* `AdSignalingModeOpportunityGenerator` 지정된 광고 신호 모드에 대한 초기 기회를 생성합니다. 큐 또는 시간 지정 메타데이터 정보는 무시됩니다.
* `CustomMarkerOpportunityGenerator` 구운 C3 광고를 대체할 수 있는 기회를 생성합니다.
* `AuditudeResolver`lazy and resolving이 켜져 있으면 기회 생성기가 기회를 생성합니다.

TVSDK에는 기본 컨텐츠 확인기도 포함되어 있습니다.

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`Primetime 광고 의사 결정 기능과 통신할 수 있습니다.

다음과 같은 방법으로 광고 워크플로우를 사용자 지정하기 위해 기본 기회 생성기 및 컨텐츠 해상도를 재정의할 수 있습니다.

* 광고 삽입에 사용할 사용자 정의 태그 인식
* 사용자 정의된 광고 공급자를 만듭니다.
* 컨텐츠를 보이지 않게 합니다.