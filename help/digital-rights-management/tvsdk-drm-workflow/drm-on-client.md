---
title: 클라이언트의 Primetime DRM
description: 클라이언트의 Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# 클라이언트의 Primetime DRM{#primetime-drm-on-the-client}

보호된 콘텐츠를 재생하는 Primetime TVSDK 애플리케이션은 우선 Primetime DRM API로 전화하여 라이선스 사용 및 보호된 콘텐츠 재생 워크플로우를 시작해야 합니다. 이 워크플로우에서 클라이언트에 대한 Primetime DRM이 보호된 콘텐츠의 메타데이터로부터 라이선스 요청을 생성한 후 이를 Primetime DRM 라이선스 서버로 보냅니다.

라이센스 요청을 실행하기 전에 클라이언트는 필요한 인증/인증을 선택적으로 수행할 수 있습니다(비즈니스 규칙에 따라).
