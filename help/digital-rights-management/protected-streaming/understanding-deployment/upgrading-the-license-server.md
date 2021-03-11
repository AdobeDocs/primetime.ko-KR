---
title: 안전한 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드
description: 안전한 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 업그레이드{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

보호된 스트리밍을 위해 Primetime DRM Server를 실행하는 서버를 업그레이드하려는 경우 응용 프로그램 서버에 배포된 `flashaccessserver.war` 파일을 최신 Primetime DRM에 포함된 파일로 바꿔야 합니다.

새 구성 옵션을 사용하려면 서버의 `flashaccess-tenant.xml`을 업데이트해야 합니다. 또한 최신 Primetime DRM에 포함된 버전으로 [!DNL jsafe.dll] 또는 [!DNL libjsafe.so]을(를) 업데이트해야 합니다.
