---
description: TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.
seo-description: TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.
seo-title: VOD 광고 확인 및 삽입
title: VOD 광고 확인 및 삽입
uuid: 69853c16-e252-472e-b33a-7a0e0c4b95dd
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# VOD 광고 해결 및 삽입{#resolve-and-insert-vod-ad}

TVSDK는 VOD(Video-On-Demand) 컨텐츠의 경우 기본 컨텐츠에 광고를 분할하여 타임라인 기간이 늘어나게 함으로써 광고 중단이 삽입됩니다.

재생 전에 TV SDK는 Adobe Primetime 광고 결정 시 반환되는 타임라인에서 설명한 대로 기본 컨텐츠에 알려진 광고를 확인하고 광고 나누기를 삽입하며 필요한 경우 가상 타임라인을 재계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **프리롤** - 컨텐츠 앞에 배치됩니다.
* **중간 롤로**, 컨텐츠의 중간에 있습니다.
* **컨텐츠 뒤에 배치되는 포스트롤**.

>[!TIP]
>
>재생이 시작되면 컨텐츠에 추가 변경 사항이 발생하지 않습니다.

광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 환경을 제공하기 위해 컨텐트에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

