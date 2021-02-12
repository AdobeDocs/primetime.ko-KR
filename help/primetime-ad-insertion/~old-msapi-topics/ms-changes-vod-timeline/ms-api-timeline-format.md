---
description: 형식화된 광고 및 pods라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.
seo-description: 형식화된 광고 및 pods라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.
seo-title: VOD 타임라인 포맷
title: VOD 타임라인 포맷
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# VOD 타임라인 형식 {#vod-timeline-format}

형식화된 광고 및 pods라는 컨텐츠 세그먼트 목록을 사용하여 VOD 컨텐츠에서 광고 중단의 타임라인을 지정하거나 재정의할 수 있습니다.

## 창 {#section_606E9456E25E41C8B8537A023DDD96CE}

창은 광고 구분이거나 컨텐츠 세그먼트입니다. 타임라인은 세미콜론으로 구분된 창 시퀀스로 구성됩니다. 다음과 같은 유형의 창이 있습니다.

### 광고 나누기

```
B,duration,maximum_number_of_ads,position
```

지속 시간은 초 단위로, 정밀도는 0.001(밀리초)입니다.광고 수는 정수입니다. 위치는 다음 중 하나입니다.
* **n** 없음 — 광고 없음
* **p** 프리롤 — 내용 앞에
* **m** 중간 롤 — 컨텐츠 내
* **t** 포스트롤 — 컨텐츠 뒤에

예를 들어 `B,60,2,p`은 컨텐츠 앞에 최대 2개의 광고에 대한 1분 분리를 나타냅니다.

### 컨텐츠 세그먼트 - 장

```
C,duration,number_of_lots
```

지속 시간은 초 단위로, 정밀도는 0.001(밀리초)입니다.로트 수(컨텐츠 섹션)는 정수입니다. 예를 들어 `C,300,1`은 컨텐츠의 단일 5분 섹션을 나타냅니다.