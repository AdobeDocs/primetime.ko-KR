---
description: VMAP 인라인 광고에 잘못된 미디어 유형이 포함되어 있는 경우 폴백을 활성화할 수 있습니다.
title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# VMAP 인라인 광고 {#define-fallback-ad-behavior-for-vmap-inline-ads}에 대한 대체 광고 비헤이비어 정의

VMAP 인라인 광고에 잘못된 미디어 유형이 포함되어 있는 경우 폴백을 활성화할 수 있습니다.

1. 선형/인라인 광고에 대한 미디어 유형이 HLS에 대해 유효하지 않을 때 VMAP이 뒤로 돌아가도록 `setFallbackOnInvalidCreativeEnabled`을(를) `true`으로 설정합니다.

   기본값은 `false`입니다. 선형 광고가 잘못된 미디어 유형이거나 광고를 다시 패키지화할 수 없기 때문에 실패하는 경우, 이 플래그를 사용하면 Primetime 광고 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
