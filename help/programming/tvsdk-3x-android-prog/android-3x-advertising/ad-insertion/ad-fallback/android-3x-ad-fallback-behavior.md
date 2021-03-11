---
description: Primetime 광고 결정 시 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)가 발견되면 반환할 내용을 결정하기 위해 폴백 광고를 평가합니다.
title: VAST 및 VMAP에 대한 광고 폴백 동작
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# VAST 및 VMAP {#ad-fallback-behavior-for-vast-and-vmap}에 대한 광고 폴백 동작

Primetime 광고 결정 시 비어 있거나 HLS에 유효하지 않은 미디어 유형이 있는 VAST 광고(크리에이티브)가 발견되면 반환할 내용을 결정하기 위해 폴백 광고를 평가합니다.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

TVSDK에서 유효한 미디어 유형은 `application/x-mpegURL`(M3U8)뿐입니다.

독립 실행형 폴백 광고가 있는 경우 Primetime 광고 결정 플러그인은 다음 순서로 이러한 광고를 검사하고 유효한 미디어 유형의 첫 번째 광고를 반환합니다.

1. 재패키징이 활성화되면 미디어 유형이 잘못된 광고의 첫 번째 발생을 다른 잘못된 미디어 유형으로 취급합니다.

   재패키징에 실패하면 이 프로세스는 광고의 추가 발생 시 적용됩니다.
1. TVSDK에서 유효한 대체 광고를 찾을 수 없으면 잘못된 미디어 유형의 원래 광고를 반환합니다.
1. 원본 광고 대신 유효한 MIME 유형의 대체 광고가 반환되는 경우 Primetime 광고 결정 시 오류 코드 403이 VAST 오류 URL로 전송됩니다(가능한 경우).
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형이 있는 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 비헤이비어는 VAST 래퍼의 광고에 대해 항상 활성화되어 있습니다. VMAP의 VAST 광고 인라인에서는 기본적으로 비헤이비어가 비활성화되지만 응용 프로그램에서 이를 활성화할 수 있습니다.