---
seo-title: 보호된 컨텐츠에 액세스할 수 없도록 제한된 애플리케이션 런타임 차단 목록
title: 보호된 컨텐츠에 액세스할 수 없도록 제한된 애플리케이션 런타임 차단 목록
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 보호된 컨텐츠에 액세스할 수 없도록 제한된 애플리케이션 런타임 차단 목록 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

콘텐츠에 액세스할 수 없는 Primetime 또는 Flash 런타임 버전을 지정합니다. 제한된 런타임(Flash Player, AIR 또는 iOS), 플랫폼 및 버전을 지정합니다.

사용 사례 예: DRM 클라이언트 차단 목록과 유사한 최신 버전의 Flash Player, AIR 또는 iOS 런타임은 라이선스 취득 및 컨텐츠 재생에 필요한 최소 버전으로 지정할 수 있습니다.

다음 속성 외에 DRM 클라이언트 버전에 지원되는 모든 속성으로 애플리케이션 런타임을 식별할 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 애플리케이션 | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | 정확히 일치 | 응용 프로그램 런타임의 이름을 식별합니다. |
