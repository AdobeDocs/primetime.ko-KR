---
description: VOD 컨텐츠 재생 중 하나에 적합한 광고 타임라인은 후속 재생에 부적절할 수 있습니다. 콘텐츠를 변경하지 않고 VOD 타임라인을 교체할 수 있습니다.
title: VOD 변경 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# VOD {#changes-to-vod} 변경 사항

VOD 컨텐츠 재생 중 하나에 적합한 광고 타임라인은 후속 재생에 부적절할 수 있습니다. 콘텐츠를 변경하지 않고 VOD 타임라인을 교체할 수 있습니다.

VOD 타임라인을 대체할 수 있는 상황은 다음과 같습니다.

* 로컬 광고를 대체하지만 C3 창 동안에는 국가 광고를 그대로 두십시오.
* C3 창이 닫힌 후 번진 광고를 바꿉니다.
* 기존 C3 광고를 보다 긴 기간의 새로운 광고로 동적으로 바꿉니다.
* 광고를 적게 삽입하거나 전혀 삽입할 수 없습니다.

새 광고 삽입 요청을 원본 M3U8 파일과 `pttimeline` 쿼리 매개 변수의 다른 값으로 제출하여 광고 타임라인을 바꿀 수 있습니다.