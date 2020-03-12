---
description: 'TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다 '
seo-description: 'TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다 '
seo-title: 크리에이티브 선택 규칙 적용
title: 크리에이티브 선택 규칙 적용
uuid: 3949bc24-3060-408b-adae-947be790a8ff
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 크리에이티브 선택 규칙 적용{#applying-creative-selection-rules}

TVSDK는 다음과 같은 방법으로 크리에이티브 선택 규칙을 적용합니다.

* TVSDK는 먼저 모든 `default` 규칙을 적용하고 영역별 규칙을 따릅니다.
* TVSDK는 현재 영역 ID에 대해 정의되지 않은 규칙을 무시합니다.
* TVSDK가 기본 규칙을 적용하면 영역별 규칙은 규칙에서 선택한 크리에이티브의 `host` (도메인)와 일치에 따라 크리에이티브 우선 순위를 추가로 변경할 수 `default` 있습니다.

* 추가 영역 규칙이 있는 포함된 샘플 규칙 파일에서 TVSDK가 `default` 규칙을 적용하면, M3U8 크리에이티브 도메인에 포함되지 [!DNL my.domain.com] 않거나 광고 영역이 있는 경우, 크리에이티브가 순서가 [!DNL a.bcd.com] `1234`다시 지정되고 사용 가능한 경우 Flash VPAID 크리에이티브가 먼저 재생됩니다. 그렇지 않으면 MP4 광고가 재생되고 JavaScript로 내려갑니다.

* 광고 크리에이티브가 선택된 경우 TVSDK가 기본적으로 재생( [!DNL .mp4][!DNL .flv]등)되지 않으면 TVSDK가 재패키징 요청을 발행합니다.

TVSDK에서 처리할 수 있는 광고 유형은 여전히 의 `validMimeTypes` 설정을 통해 정의됩니다 `AuditudeSettings`.
