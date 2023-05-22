---
description: 기회 감지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 콘텐츠 해결사로 전송되며, 이는 배치 기회 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
title: 영업 기회 감지기 및 콘텐츠 해결자 사용자 정의
exl-id: 0721278c-e128-4afc-ae81-4f23c2644859
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 개요 {#customize-opportunity-detectors-and-content-resolvers-overiew}

기회 감지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 TVADK 구성 요소입니다. 이러한 기회는 콘텐츠 해결사로 전송되며, 이는 배치 기회 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

TVSDK에는 기본 영업 기회 감지기가 포함되어 있습니다.

* `SpliceOutOpportunityDetector`: 기본 광고 큐를 이해합니다
* `AdSignalingModeOpportunityGenerator`: 광고 시그널링 모드를 기반으로 초기 광고 배치 기회를 만드는 역할을 합니다
* `SpliceOutOpportunityGenerator`: 모든 #EXT-X-CUE 태그에서 광고 배치 기회를 만드는 역할을 합니다

TVSDK에는 플레이어 항목의 메타데이터 키를 기반으로 삽입할 콘텐츠를 제공하는 기본 콘텐츠 해결자도 포함되어 있습니다.

* `AuditudeResolver`를 사용하여 Adobe Primetime 광고 결정(이전의 Auditude) 서버와 통신할 수 있으며, 배치될 광고 브레이크를 반환할 수 있습니다.

기본 영업 기회 감지기 및 콘텐츠 해결자를 재정의하여 다음과 같은 방법으로 광고 워크플로를 사용자 지정할 수 있습니다.

* 사용자 지정 태그 검색에 대한 지원 추가
* 광고 삽입에 대한 사용자 지정 태그 인식
* 사용자 지정된 광고 공급자 만들기
* 콘텐츠 차단
