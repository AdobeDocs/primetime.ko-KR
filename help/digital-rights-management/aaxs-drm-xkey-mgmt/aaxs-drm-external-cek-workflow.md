---
seo-title: AAXS DRM 외부 CEK 워크플로우
title: AAXS DRM 외부 CEK 워크플로우
description: 이 워크플로우는 중앙 저장소 또는 CKMS(Content Key Management System)를 사용하지 않아도 되기 때문에 대부분의 기존 DRM 시스템에서 벗어난 것입니다
seo-description: 이 워크플로우는 중앙 저장소 또는 CKMS(Content Key Management System)를 사용하지 않아도 되기 때문에 대부분의 기존 DRM 시스템에서 벗어난 것입니다
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# AAXS DRM 외부 CEK 워크플로{#aaxs-drm-external-cek-workflow}

이 워크플로우는 중앙 저장소 또는 CKMS(Content Key Management System)를 사용하지 않아도 되기 때문에 대부분의 기존 DRM 시스템과 다릅니다. 그러나 AAXS가 기존 CKMS와 함께 작업하기를 원하는 고객의 경우 AAXS는 &quot;외부 CEK&quot;라는 기능을 제공하며 CEK는 패키징 및 라이선스 발급 시 외부에서 제공됩니다.

![](assets/ECEK_Workflow.PNG)

1. (패키지) AAXS Java SDK에는 CEK 및 CEK ID가 제공됩니다.
1. (패키지) CEK는 컨텐츠를 암호화하는 데 사용됩니다.
1. (패키지) CEK ID가 컨텐츠의 DRM 메타데이터에 삽입됩니다.
1. 장치가 AAXS 서버에서 라이센스를 요청하여 콘텐츠를 재생하려고 합니다.
1. (라이센스) AAXS 서버는 컨텐츠 메타데이터에서 CEK ID를 추출합니다.
1. AAXS 서버는 CKMS에서 CEK를 검색합니다.
1. (라이센스) AAXS 서버는 CEK가 포함된 라이센스를 장치에 발행합니다.
