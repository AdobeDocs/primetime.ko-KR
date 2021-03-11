---
description: 기회 탐지기는 스트림에서 사용자 정의 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 컨텐츠 해결 프로그램으로 보내져 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
title: 기회 탐지 및 컨텐츠 해상도 사용자 정의
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 개요 {#customize-opportunity-detectors-and-content-resolvers-overiew}

기회 탐지기는 스트림에서 사용자 정의 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 컨텐츠 해결 프로그램으로 보내져 배치 기회 속성 및 메타데이터를 기반으로 컨텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

TVSDK에는 다음과 같은 기본 기회 탐지기가 포함되어 있습니다.

* `SpliceOutOpportunityDetector`기본 광고 큐를 이해하는
* `AdSignalingModeOpportunityGenerator`, 광고 신호 모드를 기반으로 초기 광고 배치 기회를 생성하는 책임
* `SpliceOutOpportunityGenerator`, #EXT-X-CUE 태그에서 광고 배치 기회를 만드는 책임입니다.

또한 TVSDK에는 플레이어 항목의 메타데이터 키를 기반으로 삽입할 컨텐츠를 제공하는 기본 컨텐츠 확인자도 포함되어 있습니다.

* `AuditudeResolver`, Adobe Primetime 광고 결정(이전의 Auditude) 서버와 통신하고 배치할 광고 나누기를 반환할 수 있습니다.

다음과 같은 방법으로 광고 워크플로우를 사용자 지정하기 위해 기본 기회 탐지 및 컨텐츠 해상도를 재정의할 수 있습니다.

* 사용자 지정 태그 감지에 대한 지원 추가
* 광고 삽입에 사용할 사용자 정의 태그 인식
* 맞춤형 광고 공급자 만들기
* 콘텐츠 검출

