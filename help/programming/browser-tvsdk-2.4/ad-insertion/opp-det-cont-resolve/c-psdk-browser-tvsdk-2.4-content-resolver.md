---
description: 기회 감지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 브라우저 TVSDK 구성 요소입니다. 이러한 기회는 콘텐츠 해결사로 전송되며, 이는 배치 기회 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.
title: 영업 기회 감지기 및 콘텐츠 해결자 사용자 정의
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 개요 {#customize-opportunity-detectors-and-content-resolvers-overview}

기회 감지기는 스트림의 사용자 지정 태그를 감지하고 배치 기회를 식별하는 브라우저 TVSDK 구성 요소입니다. 이러한 기회는 콘텐츠 해결사로 전송되며, 이는 배치 기회 속성 및 메타데이터를 기반으로 콘텐츠/광고 삽입 워크플로우를 사용자 정의합니다.

브라우저 TVSDK에는 다음과 같은 기본 영업 기회 감지기가 포함되어 있습니다.

* `AdSignalingModeOpportunityGenerator`: 광고 시그널링 모드를 기반으로 초기 광고 배치 기회를 만듭니다.
* `ManifestCuesOpportunityGenerator`: 모든 스플라이스 아웃 태그에서 광고 배치 기회를 만듭니다.

브라우저 TVSDK에는 다음과 같은 기본 콘텐츠 해결사도 포함됩니다. `AuditudeResolver`플레이어 항목의 메타데이터 키를 기반으로 삽입할 콘텐츠를 제공합니다. `AuditudeResolver` 는 Adobe Primetime ad decisioning 서버와 통신하고 배치할 광고 브레이크를 반환할 수 있습니다.

기본 영업 기회 감지기 및 콘텐츠 해결자를 재정의하여 다음과 같은 방법으로 광고 워크플로를 사용자 지정할 수 있습니다.

* 사용자 지정 태그 검색에 대한 지원 추가
* 광고 삽입에 대한 사용자 지정 태그 인식
* 사용자 지정된 광고 공급자 만들기
