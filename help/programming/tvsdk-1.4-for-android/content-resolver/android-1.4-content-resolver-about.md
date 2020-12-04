---
description: 기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVSDK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.
seo-description: 기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVSDK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.
seo-title: 기회 생성기 및 컨텐츠 해결
title: 기회 생성기 및 컨텐츠 해결
uuid: 593de6c0-042d-4a05-82d7-056a9a4500f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Opportunity 생성기 및 컨텐츠 해상도 {#opportunity-generators-and-content-resolvers}

기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVSDK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.

TVSDK에는 기본 기회 탐지기 기능이 포함되어 있습니다.

* `SpliceOutPlacementOpportunityDetector`, 기본 광고 큐를 이해하는 경우

또한 TVSDK에는 플레이어 항목의 메타데이터 키를 기반으로 삽입되는 컨텐츠를 제공하는 기본 컨텐츠 해상도도 포함되어 있습니다.

* `AuditudeResolver` for  `AUDITUDE_METADATA_KEY`that is capable to communication with Adobe Primetime ad decision (이전에는 Auditude) server and returning ad breaks to be placed.

* `MetadataResolver` for  `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` for  `TIME_RANGES_METADATA_KEY`

다음과 같은 방법으로 기본 기회 탐지기와 컨텐츠 해상도를 무시하여 광고 워크플로우를 사용자 정의할 수 있습니다.

* 사용자 지정 태그 검색에 대한 지원 추가
* 광고 삽입에 사용할 사용자 정의 태그 인식
* 맞춤형 광고 공급자 만들기
* 콘텐츠 검출

TVSDK는 타임라인에 광고를 배치하는 기본 기회 생성기 및 컨텐츠 해상도를 제공하며 이러한 생성기 및 해상도는 매니페스트에 있는 비표준 태그를 기반으로 합니다. 애플리케이션에서 일시 중단 기간의 표시기 등 매니페스트에서 식별된 기회에 따라 타임라인을 변경해야 할 수 있습니다.

*`opportunity`*&#x200B;은 일반적으로 광고 배치 기회를 나타내는 타임라인의 관심 영역을 나타냅니다. 이 기회는 일시 중단 기간과 같이 타임라인에 영향을 줄 수 있는 사용자 지정 작업을 나타낼 수도 있습니다. *`opportunity generator`*&#x200B;은 타임라인에서 특정 기회(태그)를 식별하고 TVSDK에 이러한 기회들에 태그가 지정되었음을 알립니다. HLS가 아닌 비표준 태그를 포함하여 타임라인에서 기회가 식별됩니다.

애플리케이션에 기회(태그)에 대한 알림을 받으면 애플리케이션이 광고 시리즈를 삽입하거나 대체 스트림(일시 중단)으로 전환하거나 타임라인 컨텐츠를 편집하여 타임라인을 변경할 수 있습니다. 기본적으로 TVSDK는 필요한 타임라인 변경 사항 또는 작업을 구현하기 위해 적절한 *`content resolver`*&#x200B;을 호출합니다. 응용 프로그램은 기본 TVSDK 광고 내용 확인자를 사용하거나 자체 컨텐츠 확인자를 등록할 수 있습니다.

또한 `MediaPlayerItemConfig.setAdTags`을(를) 사용하여 TVSDK가 `MediaPlayerItemConfig.subscribedTags`을(를) 인식하고 사용할 수 있도록 광고 마커 태그/큐를 추가하고 광고 워크플로우 정보가 있을 수 있는 추가 태그에 대해 응용 프로그램에 알릴 수도 있습니다.

사용자 지정 확인자의 사용 가능한 하나는 일시 중단 기간입니다. 이러한 기간을 처리하기 위해 애플리케이션에서 일시 중단 태그를 처리하는 권한을 가진 일시 중단 기회 탐지기 구현 및 등록할 수 있습니다. TVSDK에서 이 태그가 발견되면 등록된 모든 컨텐츠 해상도를 폴링하여 지정된 태그를 처리하는 첫 번째 컨텐츠를 찾습니다. 이 예에서는 일시 중단 컨텐츠 해결 프로그램이 있는데, 이 해결 프로그램은 현재 항목을 태그로 지정된 기간 동안 플레이어에서 대체 컨텐츠로 바꿀 수 있습니다.
