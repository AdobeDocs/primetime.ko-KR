---
description: TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-description: TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.
seo-title: VOD 광고 확인 및 삽입
title: VOD 광고 확인 및 삽입
uuid: 33280792-ad08-41c1-b180-cc2159e8137c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# VOD 광고 확인 및 삽입{#vod-ad-resolving-and-insertion}

TV VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고 브레이크를 삽입합니다.

재생 전에 TVSDK는 알려진 광고를 확인하고 Adobe Primetime 광고 결정에서 반환되는 타임라인에서 설명한 대로 기본 컨텐츠에 광고 나누기를 삽입하고 필요한 경우 가상 타임라인을 다시 계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **컨텐츠 앞에 있는 프리롤**.
* **컨텐츠에 있는 중롤**.
* **컨텐츠 뒤에 있는 포스트롤**.

재생이 시작되면 컨텐츠에서 추가로 변경할 수 없습니다. 광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 경험을 제공하기 위해 컨텐츠에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

