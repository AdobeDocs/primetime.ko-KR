---
title: 표준 AAXS DRM 워크플로우
description: 표준 AAXS DRM 워크플로우
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 표준 AAXS DRM 워크플로우{#standard-aaxs-drm-workflow}

1. (패키지) AAXS Java SDK는 무작위 CEK를 생성합니다.
1. (패키지) CEK는 콘텐츠를 암호화하는 데 사용됩니다.
1. (패키지) CEK는 AAXS 라이선스 서버의 공개 키를 사용하여 암호화됩니다.
1. (패키지) 암호화된 CEK는 콘텐츠의 DRM 메타데이터에 삽입됩니다.
1. 장치는 AAXS 서버에 라이센스를 요청하여 컨텐츠 재생을 시도합니다.
1. (라이선스) AAXS 서버는 개인 키를 사용하여 메타데이터에서 CEK를 해독합니다.
1. (라이선스) AAXS 서버는 CEK가 포함된 라이선스를 장치에 발행합니다.
