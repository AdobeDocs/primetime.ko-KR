---
keywords: 크리에이티브 선택 규칙;AdobeTVSDKConfig
title: 크리에이티브 선택 규칙 적용
description: 크리에이티브 선택 규칙 적용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 크리에이티브 선택 규칙 적용 {#apply-creative-selection-rules}

TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다.

* TVSDK는 먼저 모든 `default` 규칙을 적용하고 영역별 규칙을 따릅니다.
* TVSDK는 현재 영역 ID에 대해 정의되지 않은 규칙을 무시합니다.
* TVSDK가 기본 규칙을 적용하면 영역 특정 규칙은 `default` 규칙에서 선택한 크리에이티브 항목에 대해 `host`(도메인)에 일치하는 크리에이티브 우선순위를 추가로 변경할 수 있습니다.

* 추가 영역 규칙이 있는 포함된 샘플 규칙 파일에서 TVSDK가 `default` 규칙을 적용하면 M3U8 크리에이티브 도메인에 `my.domain.com` 또는 `a.bcd.com`이(가) 포함되어 있지 않고 광고 영역이 `1234`이면 크리에이티브가 다시 정렬되고 Flash VPAID 크리에이티브가 가능한 경우 먼저 재생됩니다. 그렇지 않으면 MP4 광고가 재생되고 JavaScript로 내려갑니다.

* 광고 크리에이티브가 선택된 상태에서 TVSDK가 기본적으로 재생되지 않는 경우( [!DNL .mp4], [!DNL .flv] 등), TVSDK는 재패키징 요청을 생성합니다.

TVSDK에서 처리할 수 있는 광고 유형은 `AuditudeSettings`의 `validMimeTypes` 설정을 통해 여전히 정의됩니다.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

