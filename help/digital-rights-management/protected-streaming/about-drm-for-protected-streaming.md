---
description: Protected Streaming용 Adobe Primetime DRM 서버는 Primetime DRM SDK를 기반으로 하는 라이선스 서버 구현입니다. 이 서버는 Primetime DRM 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발급합니다.
title: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 정보
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 정보{#about-adobe-primetime-drm-server-for-protected-streaming}

Protected Streaming용 Adobe Primetime DRM 서버는 Primetime DRM SDK를 기반으로 하는 라이선스 서버 구현입니다. 이 서버는 Primetime DRM 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발급합니다.

보호 스트리밍용 Primetime DRM 서버는 여러 테넌트를 지원합니다. 여러 콘텐츠 게시자를 대신하여 각각 고유한 구성 설정이 있는 단일 서버를 호스팅할 수 있습니다. 또한 서버는 사용자 지정 인증 구성 요소를 지원하므로 라이센스가 발급되기 전에 사용자 지정 로직을 실행할 수 있습니다.

이 서버는 HTTP 스트리밍에 사용하기 위한 것입니다. 따라서 이 서버 구현은 Primetime DRM에서 사용할 수 있는 모든 기능을 지원하지 않습니다. 예를 들어 사용자 인증 요청, 여러 정책, 도메인 바인딩된 라이선스, 라이선스 체인 또는 동기화 메시지를 지원하지 않습니다.

>[!NOTE]
>
>Adobe Primetime DRM은 이전에 Adobe 액세스라고 하였으며, 그 이전에는 Flash Access 입니다.
