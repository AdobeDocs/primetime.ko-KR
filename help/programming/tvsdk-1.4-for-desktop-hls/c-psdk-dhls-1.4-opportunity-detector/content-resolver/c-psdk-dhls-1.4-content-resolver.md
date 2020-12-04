---
description: 기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.
seo-description: 기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.
seo-title: 기회 탐지 및 컨텐츠 해상도 사용자 정의
title: 기회 탐지 및 컨텐츠 해상도 사용자 정의
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 개요 {#customize-opportunity-detectors-and-content-resolvers-overiew}

기회 탐지기는 스트림에서 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 지정하는 컨텐츠 해결 프로그램으로 전송됩니다.

TVSDK에는 다음과 같은 기본 기회 감지기가 포함되어 있습니다.

* `SpliceOutOpportunityDetector`, 기본 광고 큐를 이해하는 경우
* `AdSignalingModeOpportunityGenerator`, 광고 신호 모드를 기반으로 초기 광고 배치 기회를 만드는 책임
* `SpliceOutOpportunityGenerator`, which responsible for creating ad placement opportunity from any #EXT-X-CUE tag

또한 TVSDK에는 플레이어 항목의 메타데이터 키를 기반으로 삽입할 컨텐츠를 제공하는 기본 컨텐츠 확인자도 포함되어 있습니다.

* `AuditudeResolver`, - Adobe Primetime 광고 결정(이전의 Auditude) 서버와 통신하고 배치할 광고 차단 반환

다음과 같은 방법으로 기본 기회 탐지기와 컨텐츠 해상도를 무시하여 광고 워크플로우를 사용자 정의할 수 있습니다.

* 사용자 지정 태그 검색에 대한 지원 추가
* 광고 삽입에 사용할 사용자 정의 태그 인식
* 맞춤형 광고 공급자 만들기
* 콘텐츠 검출

