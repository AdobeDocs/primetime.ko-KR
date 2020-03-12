---
seo-title: 클라이언트의 Primetime DRM
title: 클라이언트의 Primetime DRM
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 클라이언트의 Primetime DRM{#primetime-drm-on-the-client}

보호된 콘텐츠를 재생하는 Primetime TVSDK 애플리케이션은 우선 Primetime DRM API로 전화하여 라이선스 소비 및 보호된 콘텐츠 재생 워크플로우를 시작해야 합니다. 이 워크플로우에서 클라이언트의 Primetime DRM은 보호된 콘텐츠의 메타데이터로부터 라이선스 요청을 생성한 다음 Primetime DRM 라이선스 서버로 보냅니다.

라이센스 요청을 실행하기 전에 클라이언트는 필요한 인증/인증을 선택적으로 수행할 수 있습니다(비즈니스 규칙에 따라 다름).
