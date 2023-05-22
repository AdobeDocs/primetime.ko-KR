---
title: 애플리케이션 실행 시간 차단 목록
description: 애플리케이션 실행 시간 차단 목록
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 애플리케이션 실행 시간 차단 목록 {#blocklist-of-application-runtimes}

응용 프로그램 런타임 차단 목록은 콘텐츠에 액세스할 수 없는 Primetime 클라이언트 또는 Flash 런타임의 버전을 지정합니다. 제한된 런타임(Flash Player, AIR 또는 iOS), 플랫폼 및 버전을 지정합니다.

사용 사례: Primetime DRM 클라이언트 차단 목록과 마찬가지로 Flash Player, AIR 또는 iOS 런타임의 최신 버전을 라이선스 획득 및 컨텐츠 재생에 필요한 최소 버전으로 지정할 수 있습니다.

Primetime DRM 클라이언트 버전에 대해 지원되는 속성과 다음 속성을 사용하여 응용 프로그램 런타임을 식별할 수 있습니다.

| **속성** | **지원되는 값** | **일치 기준** | **설명** |
|---|---|---|---|
| 애플리케이션 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 정확한 일치 | 응용 프로그램 런타임의 이름을 식별합니다. |
