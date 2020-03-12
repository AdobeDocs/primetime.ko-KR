---
description: 기회 생성기는 스트림의 사용자 정의 태그, 신호 모드 사용자 정의 마커 등을 기준으로 배치 기회를 식별합니다. 영업 기회 생성기는 이러한 배치 기회를 컨텐츠 해결 프로그램에 전송하여 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
seo-description: 기회 생성기는 스트림의 사용자 정의 태그, 신호 모드 사용자 정의 마커 등을 기준으로 배치 기회를 식별합니다. 영업 기회 생성기는 이러한 배치 기회를 컨텐츠 해결 프로그램에 전송하여 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
seo-title: 기회 생성기 및 컨텐츠 해결기 사용자 정의
title: 기회 생성기 및 컨텐츠 해결기 사용자 정의
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 개요 {#customize-opportunity-generators-and-content-resolvers-overview}

기회 생성기는 스트림의 사용자 정의 태그, 신호 모드 사용자 정의 마커 등을 기준으로 배치 기회를 식별합니다. 영업 기회 생성기는 이러한 배치 기회를 컨텐츠 해결 프로그램에 전송하여 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

TVSDK에는 다음과 같은 기본 기회 생성기가 포함되어 있습니다.

* `ManifestCuesOpportunityGenerator` 기본 광고 큐에서 기회를 생성합니다( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` 지정된 광고 신호 모드에 대한 초기 기회를 생성합니다. 이렇게 하면 큐 또는 시간 제한 메타데이터 정보가 무시됩니다.
* `CustomMarkerOpportunityGenerator` 구운 C3 광고를 대체할 수 있는 기회를 생성합니다.
* `AuditudeResolver`Adobe Opportunity Generator는 레이지 광고 해결 기능이 켜져 있을 때 기회를 창출합니다.

TVSDK에는 기본 컨텐츠 해상도도 포함되어 있습니다.

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`Primetime 광고 의사 결정과 통신할 수 있습니다.

기본 기회 생성기 및 컨텐츠 해결기를 대체하여 다음과 같은 방법으로 광고 워크플로우를 사용자 정의할 수 있습니다.

* 광고 삽입을 위한 사용자 정의 태그 인식 자세한 내용은 기회 생성기 [및 컨텐츠 해상도 사용자 정의를 참조하십시오](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* 사용자 정의된 광고 공급자를 만듭니다.
* 콘텐츠 검출