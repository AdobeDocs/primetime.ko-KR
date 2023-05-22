---
keywords: 크리에이티브 선택 규칙;AdobeTVSDKConfig
title: 크리에이티브 선택 규칙 적용
description: 크리에이티브 선택 규칙 적용
copied-description: true
exl-id: 17d540f3-1eea-4d12-a4b4-66e7c639591f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 크리에이티브 선택 규칙 적용 {#apply-creative-selection-rules}

TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다.

* TVSDK 모두 적용 `default` 먼저 규칙을 지정하고 영역별 규칙을 지정합니다.
* TVSDK는 현재 영역 ID에 대해 정의되지 않은 규칙을 무시합니다.
* TVSDK가 기본 규칙을 적용하고 나면 영역별 규칙은 다음에 따라 크리에이티브 우선순위를 추가로 변경할 수 있습니다. `host` (도메인)은(는) 다음에 의해 선택된 크리에이티브에서 일치합니다. `default` 규칙.

* 추가 영역 규칙이 있는 포함된 샘플 규칙 파일에서 TVSDK가 `default` 규칙, M3U8 Creative 도메인에 [!DNL my.domain.com] 또는 [!DNL a.bcd.com] 및 광고 영역은 `1234`, 크리에이티브는 순서가 변경되고 가능한 경우 Flash VPAID 크리에이티브가 먼저 재생됩니다. 그렇지 않으면 MP4 광고가 재생되며, JavaScript까지 재생됩니다.

* 광고 크리에이티브를 선택한 경우 TVSDK는 기본적으로 재생할 수 없습니다( [!DNL .mp4], [!DNL .flv]등), TVSDK가 다시 패키징 요청을 발행합니다.

TVSDK에서 처리할 수 있는 광고 유형은 여전히 `validMimeTypes` 에서 설정 `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->
