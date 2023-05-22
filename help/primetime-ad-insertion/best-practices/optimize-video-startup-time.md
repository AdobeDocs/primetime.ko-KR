---
title: 비디오 시작 시간 최적화
description: 비디오 시작 시간 최적화
exl-id: 5a89c774-0fed-4378-9cf8-98c4c843ae0d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 비디오 시작 시간 최적화 개요 {#optimize-video-start-up-times}

Primetime Ad Insertion은 경로/프로토콜 최적화를 위한 캐싱 및 규칙과 같은, 비디오 시작 시간을 최적화하는 여러 가지 기능을 제공합니다. 다음은 Primetime Ad Insertion 사용 시 더 빠른 비디오 시작 시간을 보장하기 위한 몇 가지 다른 권장 사항입니다.

* CDN(Content Delivery Network)에서 모든 광고 및 컨텐츠 제공

* Primetime Ad Insertion과 CDN 간의 TLS 악수를 줄이거나 제거합니다. 자세한 내용은 [경로 및 프로토콜 최적화](optimize-routes-protocols.md).

* 광고 및 컨텐츠 조각을 동일한 CDN에서 제공

* 라이브/VOD 콘텐츠 및 매니페스트에 대한 캐시 제어 헤더 삽입

* 응답이 느린 광고 공급자 또는 광고 크리에이티브를 줄이거나 제거하십시오
