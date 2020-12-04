---
seo-title: 표준 AAXS DRM 워크플로우
title: 표준 AAXS DRM 워크플로우
description: 표준 AAXS DRM 워크플로우
seo-description: 표준 AAXS DRM 워크플로우
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 표준 AAXS DRM 워크플로우{#standard-aaxs-drm-workflow}

1. (패키지) AAXS Java SDK가 무작위 CEK를 생성합니다.
1. (패키지) CEK는 컨텐츠를 암호화하는 데 사용됩니다.
1. (패키지) AAXS 라이센스 서버의 공개 키를 사용하여 CEK가 암호화됩니다.
1. (패키지) 암호화된 CEK가 컨텐츠의 DRM 메타데이터에 삽입됩니다.
1. 장치가 AAXS 서버에서 라이센스를 요청하여 콘텐츠를 재생하려고 합니다.
1. (라이센스) AAXS 서버는 개인 키를 사용하여 메타데이터의 CEK를 해독합니다.
1. (라이센스) AAXS 서버는 CEK가 포함된 라이센스를 장치에 발행합니다.
