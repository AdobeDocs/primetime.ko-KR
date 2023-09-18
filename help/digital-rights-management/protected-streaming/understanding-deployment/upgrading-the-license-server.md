---
title: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드
description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Primetime DRM Server for Protected Streaming을 실행하는 서버를 업그레이드하려면 다음을 교체해야 합니다. `flashaccessserver.war` 최신 Primetime DRM에 포함된 파일과 함께 애플리케이션 서버에 배포된 파일입니다.

새 구성 옵션을 사용하려면 서버의 `flashaccess-tenant.xml`. 업데이트해야 합니다. [!DNL jsafe.dll] 또는 [!DNL libjsafe.so] 최신 Primetime DRM에 포함된 버전
