---
seo-title: 안전한 스트리밍을 위한 Adobe Primetime DRM Server 업그레이드
title: 안전한 스트리밍을 위한 Adobe Primetime DRM Server 업그레이드
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 안전한 스트리밍을 위한 Adobe Primetime DRM Server 업그레이드{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

보호된 스트리밍을 위한 Primetime DRM Server를 실행하는 서버를 업그레이드하려면 애플리케이션 서버에 배포된 `flashaccessserver.war` 파일을 최신 Primetime DRM에 포함된 파일로 교체해야 합니다.

새 구성 옵션을 사용하려면 서버의 내용을 업데이트해야 합니다 `flashaccess-tenant.xml`. 또한 최신 Primetime DRM에 포함된 버전을 업데이트하거나 [!DNL jsafe.dll] 업데이트해야 [!DNL libjsafe.so] 합니다.
