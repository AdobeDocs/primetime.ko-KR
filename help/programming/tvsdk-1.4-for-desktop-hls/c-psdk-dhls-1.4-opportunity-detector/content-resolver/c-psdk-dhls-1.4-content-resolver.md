---
description: 기회 탐지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 컨텐츠 해결 프로그램으로 보내져 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
seo-description: 기회 탐지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 컨텐츠 해결 프로그램으로 보내져 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
seo-title: 기회 감지기 및 컨텐츠 해상도 사용자 정의
title: 기회 감지기 및 컨텐츠 해상도 사용자 정의
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 개요 {#customize-opportunity-detectors-and-content-resolvers-overiew}

기회 탐지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 컨텐츠 해결 프로그램으로 보내져 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

TVSDK에는 기본 기회 탐지기가 포함되어 있습니다.

* `SpliceOutOpportunityDetector`, 기본 광고 큐를 이해하는
* `AdSignalingModeOpportunityGenerator`를 참조하십시오.
* `SpliceOutOpportunityGenerator`, which responsible for creating ad placement opportunity from any #EXT-X-CUE tag

TVSDK에는 플레이어 항목의 메타데이터 키를 기반으로 삽입할 컨텐츠를 제공하는 기본 컨텐츠 확인자도 포함되어 있습니다.

* `AuditudeResolver`, Adobe Primetime 광고 결정(이전의 Auditude) 서버와 통신하고 배치할 광고 차단 기능을 제공합니다.

다음과 같은 방법으로 기본 기회 탐지기와 컨텐츠 해상도를 무시하여 광고 워크플로우를 사용자 정의할 수 있습니다.

* 사용자 지정 태그 감지에 대한 지원 추가
* 광고 삽입을 위한 사용자 정의 태그 인식
* 사용자 정의된 광고 공급자 만들기
* 콘텐트 지우기

