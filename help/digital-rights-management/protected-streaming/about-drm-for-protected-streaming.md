---
description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버는 Primetime DRM SDK를 기반으로 하는 라이선스 서버 구현입니다. 이 서버는 Primetime DRM 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발행합니다.
seo-description: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버는 Primetime DRM SDK를 기반으로 하는 라이선스 서버 구현입니다. 이 서버는 Primetime DRM 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발행합니다.
seo-title: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 정보
title: 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 정보
uuid: 775bef19-6071-428f-80f5-57cae472753c
translation-type: tm+mt
source-git-commit: 68f1318db89cf9422f5969f669c11f3784560db6
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 정보{#about-adobe-primetime-drm-server-for-protected-streaming}

보호된 스트리밍을 위한 Adobe Primetime DRM 서버는 Primetime DRM SDK를 기반으로 하는 라이선스 서버 구현입니다. 이 서버는 Primetime DRM 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발행합니다.

보호된 스트리밍을 위한 Primetime DRM 서버는 여러 세입자를 지원합니다. 자체 구성 설정을 사용하여 여러 컨텐츠 게시자를 대신하여 단일 서버를 호스팅할 수 있습니다. 또한 서버가 사용자 정의 인증 구성 요소를 지원하므로 라이센스가 발급되기 전에 사용자 정의 로직을 실행할 수 있습니다.

이 서버는 HTTP 스트리밍과 함께 사용하도록 만들어졌습니다. 따라서 이 서버 구현은 Primetime DRM에서 사용 가능한 모든 기능을 지원하지 않습니다. 예를 들어 사용자 인증 요청, 여러 정책, 도메인 바인딩된 라이센스, 라이선스 체인 또는 동기화 메시지를 지원하지 않습니다.

>[!NOTE]
>
>Adobe Primetime DRM은 이전에 Adobe 액세스라고 불렸으며 그 이전에는 Flash Access으로 불렸습니다.

