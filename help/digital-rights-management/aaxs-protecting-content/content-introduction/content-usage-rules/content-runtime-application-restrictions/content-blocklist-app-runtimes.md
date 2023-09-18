---
title: 보호된 콘텐츠에 대한 액세스가 제한되는 애플리케이션 런타임 차단 목록
description: 보호된 콘텐츠에 대한 액세스가 제한되는 애플리케이션 런타임 차단 목록
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 보호된 콘텐츠에 대한 액세스가 제한되는 애플리케이션 런타임 차단 목록 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

콘텐츠에 액세스할 수 없는 Primetime 또는 Flash 런타임의 버전을 지정합니다. 제한된 런타임(Flash Player, AIR 또는 iOS), 플랫폼 및 버전을 지정합니다.

사용 사례: DRM 클라이언트 차단 목록과 마찬가지로 Flash Player, AIR 또는 iOS 런타임 최신 버전을 라이선스 획득 및 컨텐츠 재생에 필요한 최소 버전으로 지정할 수 있습니다.

응용 프로그램 런타임은 다음 속성 외에도 DRM 클라이언트 버전에 대해 지원되는 속성 중 하나로 식별될 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 애플리케이션 | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | 정확한 일치 | 응용 프로그램 런타임의 이름을 식별합니다. |
