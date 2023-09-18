---
description: Primetime ad decisioning가 비어 있거나 HLS에 대해 잘못된 미디어 유형이 있는 VAST 광고(크리에이티브)에 대한 카운터 값을 지정하면 대체 광고를 평가하여 반환할 항목을 결정합니다.
title: VAST 및 VMAP에 대한 광고 대체 동작
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# VAST 및 VMAP에 대한 광고 대체 동작 {#ad-fallback-behavior-for-vast-and-vmap}

Primetime ad decisioning가 비어 있거나 HLS에 대해 잘못된 미디어 유형이 있는 VAST 광고(크리에이티브)에 대한 카운터 값을 지정하면 대체 광고를 평가하여 반환할 항목을 결정합니다.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

TVSDK에서 유효한 미디어 유형은 다음과 같습니다. `application/x-mpegURL` (M3U8).

독립형 대체 광고가 있는 경우 Primetime ad decisioning 플러그인은 다음 순서로 이러한 광고를 검사하고 유효한 미디어 유형의 첫 번째 광고를 반환합니다.

1. 리패키징이 활성화되면 잘못된 미디어 유형의 광고가 처음 발생하는 경우 다른 잘못된 미디어 유형과 유사하게 처리됩니다.

   다시 패키징에 실패하는 경우 이 프로세스는 추가 광고 발생 횟수에 적용됩니다.
1. TVSDK에서 유효한 대체 광고를 찾지 못하면 잘못된 미디어 유형의 원래 광고가 반환됩니다.
1. 유효한 MIME 유형의 대체 광고가 원본 광고 대신 반환되는 경우, Primetime ad decisioning은 오류 코드 403을 VAST 오류 URL로 보냅니다(사용 가능한 경우).
1. 대체 광고가 래퍼이고 여러 광고를 반환하는 경우 올바른 미디어 유형의 광고만 반환됩니다.

>[!IMPORTANT]
>
>이 동작은 VAST 래퍼의 광고에 대해 항상 활성화되어 있습니다. VMAP에서 인라인된 VAST 광고의 경우, 기본적으로 비헤이비어는 비활성화되지만 애플리케이션에서 활성화할 수 있습니다.
