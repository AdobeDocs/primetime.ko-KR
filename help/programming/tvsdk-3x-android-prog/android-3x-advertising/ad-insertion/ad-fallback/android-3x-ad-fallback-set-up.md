---
description: VMAP 인라인 광고에 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.
seo-description: VMAP 인라인 광고에 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.
seo-title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# VMAP 인라인 광고에 대한 대체 광고 동작 정의 {#define-fallback-ad-behavior-for-vmap-inline-ads}

VMAP 인라인 광고에 잘못된 미디어 유형이 들어 있는 경우 폴백을 활성화할 수 있습니다.

1. 선형/인라인 광고에 대한 미디어 유형이 HLS에 대해 올바르지 않을 때 VMAP이 뒤로 `setFallbackOnInvalidCreativeEnabled` `true` 넘어가도록 설정합니다.

   기본값은 `false`입니다. 선형 광고가 잘못된 미디어 유형이나 광고를 다시 패키지할 수 없어 실패하는 경우 이 플래그를 사용하면 Primetime 광고 결정이 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따르도록 할 수 있습니다.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
