---
description: VMAP 인라인 광고에 잘못된 미디어 유형이 포함된 경우 폴백을 활성화할 수 있습니다.
title: VMAP 인라인 광고에 대한 대체 광고 동작 정의
exl-id: 57fd1b89-bcee-4c23-88e7-7a576c47c6f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# VMAP 인라인 광고에 대한 대체 광고 동작 정의 {#define-fallback-ad-behavior-for-vmap-inline-ads}

VMAP 인라인 광고에 잘못된 미디어 유형이 포함된 경우 폴백을 활성화할 수 있습니다.

1. 설정 `setFallbackOnInvalidCreativeEnabled` 끝 `true` 선형/인라인 광고의 미디어 유형이 HLS에 유효하지 않을 때 VMAP이 폴백되도록 합니다.

   기본값은 입니다. `false`. 선형 광고가 유효하지 않은 미디어 유형을 가지고 있거나 광고를 다시 패키징할 수 없기 때문에 실패하는 경우, 이 플래그를 사용하면 Primetime 광고 결정에서 광고가 빈 VAST 래퍼인 것처럼 동일한 폴백 동작을 따를 수 있습니다.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
