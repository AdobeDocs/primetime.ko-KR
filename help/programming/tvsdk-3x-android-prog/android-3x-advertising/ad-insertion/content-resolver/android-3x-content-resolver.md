---
description: 기회 생성기는 스트림의 사용자 정의 태그, 시그널링 모드 사용자 정의 마커 등으로 배치 기회를 식별합니다. 기회 생성기는 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램에 이러한 배치 기회를 보냅니다.
seo-description: 기회 생성기는 스트림의 사용자 정의 태그, 시그널링 모드 사용자 정의 마커 등으로 배치 기회를 식별합니다. 기회 생성기는 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램에 이러한 배치 기회를 보냅니다.
seo-title: 기회 생성기 및 컨텐츠 해상도 사용자 정의
title: 기회 생성기 및 컨텐츠 해상도 사용자 정의
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 개요 {#customize-opportunity-generators-and-content-resolvers-overview}

기회 생성기는 스트림의 사용자 정의 태그, 시그널링 모드 사용자 정의 마커 등으로 배치 기회를 식별합니다. 기회 생성기는 배치 기회의 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램에 이러한 배치 기회를 보냅니다.

TVSDK에는 다음과 같은 기본 기회 생성기가 포함되어 있습니다.

* `ManifestCuesOpportunityGenerator` 기본 광고 큐에서 기회( `#EXT-X-CUE`)를 생성합니다.

* `AdSignalingModeOpportunityGenerator` 지정된 광고 신호 모드에 대한 초기 기회를 생성합니다. 이는 큐 또는 시간 제한 메타데이터 정보를 무시합니다.
* `CustomMarkerOpportunityGenerator` 구운 C3 광고를 대체할 기회를 생성합니다.
* `AuditudeResolver`lazy and resolution 이 켜져 있으면 기회 창출

TVSDK에는 기본 컨텐츠 확인기도 포함되어 있습니다.

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`Primetime 광고 의사 결정 기능과 통신할 수 있습니다.

다음과 같은 방법으로 광고 워크플로우를 사용자 지정하기 위해 기본 기회 생성기 및 컨텐츠 해상도를 재정의할 수 있습니다.

* 광고 삽입을 위한 사용자 지정 태그 인식 자세한 내용은 [기회 생성기 및 컨텐츠 해상도 사용자 정의](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md)를 참조하십시오.
* 사용자 정의된 광고 공급자를 만듭니다.
* 콘텐츠 검출