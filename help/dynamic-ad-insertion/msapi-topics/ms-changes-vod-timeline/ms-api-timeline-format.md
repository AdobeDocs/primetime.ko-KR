---
description: 포맷된 광고 및 창(pods)이라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.
seo-description: 포맷된 광고 및 창(pods)이라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.
seo-title: VOD 타임라인 포맷
title: VOD 타임라인 포맷
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# VOD 타임라인 포맷 {#vod-timeline-format}

포맷된 광고 및 창(pods)이라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.

## 창 {#section_606E9456E25E41C8B8537A023DDD96CE}

창은 광고 중단이나 컨텐츠 세그먼트입니다. 타임라인은 세미콜론으로 구분된 일련의 창으로 구성됩니다. 다음과 같은 유형의 창이 있습니다.

### 광고 중단

```
B,duration,maximum_number_of_ads,position
```

지속 시간은 초 단위로, 정밀도는 0.001(밀리초)입니다.광고 수는 정수입니다. 위치는 다음 중 하나입니다.
* **n** 없음 — 광고 없음
* **p** 프리롤 — 내용 앞
* **m** mid-roll — 컨텐츠 내
* **t** 게시물-롤 — 컨텐츠 뒤

예를 들어 `B,60,2,p`은 컨텐츠 앞에 최대 2개의 광고에 대한 1분 분담을 나타냅니다.

### 컨텐츠 세그먼트 - 장

```
C,duration,number_of_lots
```

지속 시간은 초 단위로, 정밀도는 0.001(밀리초)입니다.로트 수(컨텐츠 섹션)는 정수입니다. 예를 들어 `C,300,1`은 컨텐츠의 단일 5분 섹션을 나타냅니다.