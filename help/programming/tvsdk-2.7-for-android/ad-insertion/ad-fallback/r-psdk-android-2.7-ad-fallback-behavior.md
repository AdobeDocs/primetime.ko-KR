---
description: Primetime 광고 결정이 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)를 만나면, 반환할 내용을 결정하기 위해 폴백 광고를 평가합니다.
seo-description: Primetime 광고 결정이 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)를 만나면, 반환할 내용을 결정하기 위해 폴백 광고를 평가합니다.
seo-title: VAST 및 VMAP에 대한 광고 폴백 동작
title: VAST 및 VMAP에 대한 광고 폴백 동작
uuid: 50e17372-fd29-4792-aafa-8f9c21cc42c6
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# VAST 및 VMAP {#ad-fallback-behavior-for-vast-and-vmap}에 대한 광고 폴백 동작

Primetime 광고 결정이 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)를 만나면, 반환할 내용을 결정하기 위해 폴백 광고를 평가합니다.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

TVSDK에서 유효한 미디어 유형은 `application/x-mpegURL`(M3U8)뿐입니다.

독립 실행형 폴백 광고가 있는 경우 Primetime 광고 결정 플러그인은 다음 순서로 이러한 광고를 검사하고 유효한 미디어 유형이 있는 첫 번째 광고를 반환합니다.

1. 재패키징이 활성화되면 잘못된 미디어 유형이 있는 광고의 첫 번째 발생을 다른 잘못된 미디어 유형으로 처리합니다.

   재패키징에 실패하면 이 프로세스는 추가 광고 발생 시 적용됩니다.
1. TVSDK에서 올바른 대체 광고를 찾지 못하면 잘못된 미디어 유형이 있는 원본 광고를 반환합니다.
1. 원본 광고 대신 유효한 MIME 형식의 대체 광고가 반환되는 경우 Primetime 광고 결정 시 오류 코드 403이 VAST 오류 URL로 전송됩니다.
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형을 가진 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 동작은 VAST 래퍼에서 항상 활성화됩니다. VMAP의 VAST 광고 인라인인 경우 기본적으로 비헤이비어가 비활성화되지만 애플리케이션에서 활성화할 수 있습니다.

