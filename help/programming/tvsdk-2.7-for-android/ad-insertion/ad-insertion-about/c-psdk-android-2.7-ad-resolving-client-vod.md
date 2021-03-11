---
description: VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고를 삽입합니다.
title: VOD 광고 해결 및 삽입
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# VOD 광고 해결 및 삽입 {#resolve-and-insert-vod-ad}

VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 타임라인 지속 시간이 늘어나게 기본 컨텐츠에 광고를 분할하여 광고를 삽입합니다.

재생 전에 TV SDK는 Adobe Primetime 광고 결정에서 반환되는 타임라인에서 설명한 대로 기본 컨텐츠에 알려진 광고를 확인하고 광고 나누기를 삽입하며, 필요한 경우 가상 타임라인을 재계산합니다.

TVSDK는 다음과 같은 방법으로 광고를 삽입합니다.

* **프리롤** - 컨텐츠 앞에 배치됩니다.
* **중간 롤로**, 컨텐츠의 중간에 있습니다.
* **컨텐츠 뒤에 배치되는 포스트롤**.

>[!TIP]
>
>재생이 시작되면 내용에서 추가로 변경할 수 없습니다.

광고는 다음과 같을 수 없습니다.

* 삽입됨
* 삭제됨

   예를 들어, 광고 없는 환경을 제공하기 위해 컨텐트에서 내장 광고를 삭제할 수 없습니다.
* 대체됨

   예를 들어 내장된 광고를 타깃팅된 광고로 대체할 수 없습니다.

