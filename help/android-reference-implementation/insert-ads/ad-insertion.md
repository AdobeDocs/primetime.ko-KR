---
description: 참조 구현에서는 광고 삽입에 대한 비디오 메타데이터 설정과 VOD 또는 라이브/선형 비디오 스트림에 프리롤, 미드롤 및 포스트롤 광고를 해결하는 것을 포함하는 광고 플레이어를 설정하는 방법을 보여 줍니다. 클릭 가능한 광고를 처리하는 방법도 보여줍니다.
title: 광고 삽입
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 광고 삽입 {#ad-insertion}

참조 구현에서는 광고 삽입에 대한 비디오 메타데이터 설정과 VOD 또는 라이브/선형 비디오 스트림에 프리롤, 미드롤 및 포스트롤 광고를 해결하는 것을 포함하는 광고 플레이어를 설정하는 방법을 보여 줍니다. 클릭 가능한 광고를 처리하는 방법도 보여줍니다.

광고 삽입에 대한 플레이어를 설정하는 프로세스는 다음과 같습니다.

* **입력 피드:** 광고 메타데이터로 입력 피드 채우기 [카탈로그 형식](../set-up-dev-environment/exploring-code/catalog-format.md)을 참조하십시오.
* **참조 구현 피드 어댑터:** 입력 피드를 구문 분석하여 광고 메타데이터 개체를 채웁니다.
* **AdsManager:** AdsManager를 사용하여 광고 메타데이터를 검색하고 해당 AdProvider를 만듭니다.