---
title: VOD Ad Insertion 사용
description: VOD에 Ad Insertion 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# VOD Ad Insertion 사용 {#ad-insertion-vod}

Primetime Ad Insertion은 표준 VAST 3.0+ 또는 VMAP 1.0+ 형식을 사용하여 여러 VOD 자산에 대한 광고 삽입을 지원합니다.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB 방대](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (광고 맵) {#server-mapped-ads}

Primetime Ad Insertion은 VMAP 형식으로 정의된 광고 타임라인 정보를 사용하여 재생 시작 전에 광고가 삽입된 VOD 삽입을 지원합니다.  breakStart/breakEnd 비콘과 같은 VMAP별 광고 추적은 [광고 추적](set-up-ad-tracking.md).

## 전체 이벤트 재생(Ad Decisioning 큐가 있는 VOD) {#full-event-replay}

Primetime Ad Insertion은 또한 이전에 기록된 라이브 이벤트 재생에서 발견된 것과 같이 컨텐츠 스트림 자체에 큐를 포함하는 특수 VOD 자산을 지원합니다. 지원하는 광고 결정 큐(또는 큐 형식) 유형에 대한 자세한 내용은 [라이브/선형에서 Ad Insertion 사용](ad-insertion-live-linear-stream.md).

두 개 이상의 광고 브레이크가 포함된 VOD 자산에 대해 단일 광고 요청 시나리오와 병렬 여러 광고 요청 시나리오를 모두 지원합니다. 자세한 내용은 `ptmulticall` 의 매개 변수 [매개 변수 설명](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). VAST 및 VMAP 형식은 모두 스트림 내 큐에서 지원됩니다.
