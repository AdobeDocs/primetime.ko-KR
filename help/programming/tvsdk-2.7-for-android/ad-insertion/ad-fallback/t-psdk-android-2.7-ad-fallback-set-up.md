---
description: VMAP 인라인 및 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.
seo-description: VMAP 인라인 및 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.
seo-title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# VMAP 인라인 광고 {#define-fallback-ad-behavior-for-vmap-inline-ads}에 대한 대체 광고 동작 정의

VMAP 인라인 및 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.

1. 선형/인라인 광고에 대한 미디어 유형이 HLS에 대해 유효하지 않을 때 VMAP이 뒤로 돌아가도록 `setFallbackOnInvalidCreativeEnabled`을 `true`으로 설정합니다.

   기본값은 `false`입니다. 선형 광고가 잘못된 미디어 유형이거나, 광고를 다시 패키지할 수 없기 때문에 실패하는 경우, 이 플래그를 사용하면 Primetime 광고 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

