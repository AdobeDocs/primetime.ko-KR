---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: 크리에이티브 선택 규칙 적용
title: 크리에이티브 선택 규칙 적용
uuid: 75109483-ea60-43a8-92e7-4bcba48986bc
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 크리에이티브 선택 규칙 적용 {#apply-creative-selection-rules}

TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다.

* TVSDK는 먼저 모든 `default` 규칙을 적용하고 영역별 규칙을 따릅니다.
* 현재 영역 ID에 대해 정의되지 않은 규칙은 TVSDK에서 무시됩니다.
* TVSDK가 기본 규칙을 적용하면 영역 특정 규칙은 `default` 규칙에서 선택한 크리에이티브 항목에 대해 `host`(도메인)과 일치하는 크리에이티브 우선 순위를 추가로 변경할 수 있습니다.

* 추가 영역 규칙이 있는 포함된 샘플 규칙 파일에서 TVSDK가 `default` 규칙을 적용하면 M3U8 크리에이티브 도메인에 [!DNL my.domain.com] 또는 [!DNL a.bcd.com]가 포함되지 않고 광고 영역이 `1234`인 경우 크리에이티브 순서가 재지정되고 사용 가능한 경우 Flash VPAID 크리에이티브가 먼저 재생됩니다. 그렇지 않으면 MP4 광고가 재생되고 JavaScript로 내려갑니다.

* 광고 크리에이티브가 선택된 경우 TVSDK가 기본적으로 재생될 수 없는 경우( [!DNL .mp4], [!DNL .flv] 등), TVSDK가 재패키징 요청을 발행합니다.

TVSDK에서 처리할 수 있는 광고 유형은 여전히 `AuditudeSettings`의 `validMimeTypes` 설정을 통해 정의됩니다.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

