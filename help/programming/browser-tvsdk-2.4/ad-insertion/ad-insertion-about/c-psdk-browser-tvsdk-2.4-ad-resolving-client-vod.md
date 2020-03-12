---
description: VOD(Video-On-Demand) 컨텐츠의 경우 Browser TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-description: VOD(Video-On-Demand) 컨텐츠의 경우 Browser TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-title: VOD 광고 확인 및 삽입
title: VOD 광고 확인 및 삽입
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VOD 광고 확인 및 삽입{#vod-ad-resolving-and-insertion}

VOD(Video-On-Demand) 컨텐츠의 경우 Browser TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.

재생 전에 Browser TVSDK는 Adobe Primetime 광고 결정에서 반환되는 타임라인에서 설명한 대로 알려진 광고를 확인하고 기본 컨텐츠에 광고 나누기를 삽입하고 필요한 경우 가상 타임라인을 다시 계산합니다.

브라우저 TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **컨텐츠 앞에 있는 프리롤**.
* **컨텐츠 뒤에 있는 포스트롤**.

재생이 시작되면 컨텐츠에서 추가로 변경할 수 없습니다. 광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 경험을 제공하기 위해 컨텐츠에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

