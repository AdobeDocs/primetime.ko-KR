---
title: 표준 AAXS DRM 워크플로우
description: 표준 AAXS DRM 워크플로우
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 표준 AAXS DRM 워크플로{#standard-aaxs-drm-workflow}

1. (패키지) AAXS Java SDK는 임의 CEK를 생성합니다.
1. (패키지) CEK는 컨텐츠를 암호화하는 데 사용됩니다.
1. (패키지) AAXS 라이센스 서버의 공개 키를 사용하여 CEK가 암호화됩니다.
1. (패키지) 암호화된 CEK가 내용의 DRM 메타데이터에 삽입됩니다.
1. 장치가 AAXS 서버에서 라이선스를 요청하여 콘텐츠를 재생하려고 합니다.
1. (라이센스) AAXS 서버는 메타데이터의 CEK를 해독하기 위해 개인 키를 사용합니다.
1. (라이센스) AAXS 서버는 CEK가 포함된 라이센스를 장치에 발행합니다.
