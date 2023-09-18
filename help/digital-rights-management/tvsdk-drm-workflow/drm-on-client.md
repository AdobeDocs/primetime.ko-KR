---
title: 클라이언트의 Primetime DRM
description: 클라이언트의 Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 클라이언트의 Primetime DRM{#primetime-drm-on-the-client}

보호된 콘텐츠를 재생하는 Primetime TVSDK 애플리케이션은 먼저 Primetime DRM API를 호출하여 라이선스 소비 및 보호된 콘텐츠 재생을 위한 워크플로를 시작해야 합니다. 이 워크플로에서는 클라이언트의 Primetime DRM이 보호된 콘텐츠의 메타데이터에서 라이선스 요청을 구성한 다음 Primetime DRM 라이선스 서버로 전송합니다.

라이센스 요청을 실행하기 전에 클라이언트는 비즈니스 규칙에 따라 필요한 인증/권한 부여를 선택적으로 수행할 수 있습니다.
