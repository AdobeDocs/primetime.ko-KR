---
title: 비디오 시작 시간 최적화
description: 비디오 시작 시간 최적화
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 비디오 시작 시간 최적화 개요 {#optimize-video-start-up-times}

Primetime Ad Insertion은 캐싱, 라우트/프로토콜 최적화 규칙 등 비디오 시작 시간을 최적화하는 여러 기능을 제공합니다. 다음은 Primetime Ad Insertion 사용 시 비디오 시작 시간을 단축하기 위한 몇 가지 권장 사항입니다.

* CDN(Content Delivery Network)의 모든 광고 및 콘텐츠 제공

* Primetime Ad Insertion과 CDN 간에 TLS 핸드셰이크를 줄이거나 제거합니다. 자세한 내용은 [경로 및 프로토콜 최적화](optimize-routes-protocols.md)를 참조하십시오.

* 동일한 CDN의 광고 및 컨텐츠 조각 제공

* 실시간/VOD 컨텐츠 및 매니페스트에 대한 캐시 제어 헤더 삽입

* 응답 속도가 느린 광고 공급자 또는 광고 크리에이티브 감소 또는 제거
