---
title: AAXS DRM 외부 CEK 워크플로우
description: 이 워크플로우는 중앙 저장소 또는 CKMS(Content Key Management System)를 사용할 필요가 없으므로 대부분의 기존 DRM 시스템에서 벗어납니다
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# AAXS DRM 외부 CEK 워크플로우{#aaxs-drm-external-cek-workflow}

이 워크플로우는 중앙 저장소 또는 CKMS(Content Key Management System)를 사용할 필요가 없으므로 대부분의 기존 DRM 시스템에서 벗어납니다. 다만 AAXS가 기존 CKMS와 연동하기를 원하는 고객을 위해 AAXS는 포장 및 라이선스 발급 시 CEK를 외부에 공급하는 &#39;외장형 CEK&#39;라는 기능을 제공한다.

![](assets/ECEK_Workflow.PNG)

1. (패키지) AAXS Java SDK는 CEK 및 CEK ID와 함께 제공됩니다.
1. (패키지) CEK는 콘텐츠를 암호화하는 데 사용됩니다.
1. (패키지) CEK ID는 콘텐츠의 DRM 메타데이터에 삽입됩니다.
1. 장치는 AAXS 서버에 라이센스를 요청하여 컨텐츠 재생을 시도합니다.
1. (라이선스) AAXS 서버는 콘텐츠 메타데이터에서 CEK ID를 추출합니다.
1. AAXS 서버는 CKMS에서 CEK를 검색합니다.
1. (라이선스) AAXS 서버는 CEK가 포함된 라이선스를 장치에 발행합니다.
