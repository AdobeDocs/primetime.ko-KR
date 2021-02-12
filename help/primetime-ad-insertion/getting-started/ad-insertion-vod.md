---
title: VOD용 Ad Insertion 사용
description: VOD용 Ad Insertion 사용
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# VOD {#ad-insertion-vod}에 Ad Insertion 사용

Primetime Ad Insertion은 표준 VAST 3.0+ 또는 VMAP 1.0+ 포맷을 사용하여 다양한 VOD 에셋에 광고를 삽입할 수 있도록 지원합니다.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD(광고 맵) {#server-mapped-ads}

Primetime Ad Insertion은 VMAP 포맷으로 정의된 광고 타임라인 정보를 사용하여 재생 시작 전에 삽입된 광고를 통해 VOD 삽입을 지원합니다.  breakStart/breakEnd 비콘과 같은 VMAP 특정 광고 추적은 [광고 추적](set-up-ad-tracking.md)과 함께 제공됩니다.

## 전체 이벤트 재생(Ad Decisioning 큐이 있는 VOD) {#full-event-replay}

또한 Primetime Ad Insertion은 이전에 녹화된 라이브 이벤트의 재생과 같이 콘텐츠 스트림 자체에 큐가 포함된 특화된 VOD 에셋을 지원합니다. Adobe에서 지원하는 광고 결정 큐(또는 큐 형식)의 유형에 대한 자세한 내용은 [라이브/선형](ad-insertion-live-linear-stream.md)에서 Ad Insertion 사용을 참조하십시오.

둘 이상의 광고 중단이 포함된 VOD 자산에 대해 단일 광고 요청 및 병렬 다중 광고 요청 시나리오를 모두 지원합니다. 자세한 내용은 [매개 변수 설명](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)의 `ptmulticall` 매개 변수를 참조하십시오. 스트림 큐에서 VAST 및 VMAP 형식이 모두 지원됩니다.
