---
title: 애플리케이션 런타임 차단 목록
description: 애플리케이션 런타임 차단 목록
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 응용 프로그램 런타임의 차단 목록 {#blocklist-of-application-runtimes}

응용 프로그램 런타임의 차단 목록은 콘텐츠에 액세스할 수 없는 Primetime 클라이언트 또는 Flash 런타임 버전을 지정합니다. 제한된 런타임(Flash Player, AIR 또는 iOS), 플랫폼 및 버전을 지정합니다.

사용 사례 예:Primetime DRM 클라이언트 차단 목록과 유사한 최신 버전의 Flash Player, AIR 또는 iOS 런타임은 라이선스 취득 및 컨텐츠 재생에 필요한 최소 버전으로 지정할 수 있습니다.

다음 특성 외에 Primetime DRM 클라이언트 버전에 지원되는 모든 특성을 사용하여 응용 프로그램 런타임을 식별할 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 애플리케이션 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 정확히 일치 | 응용 프로그램 런타임의 이름을 식별합니다. |

