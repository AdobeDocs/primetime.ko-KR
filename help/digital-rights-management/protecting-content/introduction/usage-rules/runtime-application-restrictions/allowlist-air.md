---
title: 보호된 콘텐츠를 재생하기 위한 Primetime DRM 응용 프로그램 허용 목록
description: 보호된 콘텐츠를 재생하기 위한 Primetime DRM 응용 프로그램 허용 목록
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Primetime DRM 응용 프로그램의 허용 목록에서 보호된 내용 재생 가능{#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

허용 목록은 내용을 재생할 수 있는 AIR, iOS 및 Android 응용 프로그램을 지정합니다. 또한 AIR 및 iOS 응용 프로그램 ID, 최소 버전, 최대 버전 및 게시자 ID를 지정합니다.

사용 사례 예:특정 응용 프로그램으로 재생을 제한하거나 콘텐트에 액세스할 수 있는 응용 프로그램 버전을 제어하려면 이 규칙을 사용합니다.

>[!NOTE]
>
>Adobe Flash Builder을 사용하여 보호된 응용 프로그램을 빌드하는 경우 [디버그] 모드에서 응용 프로그램을 배포하지 않아야 합니다. 디버그 모드에서 응용 프로그램을 배포할 때 Flash Builder이 AIR 응용 프로그램 ID에 `.debug`을(를) 추가하면 Primetime DRM의 허용 목록 기능이 예기치 않게 동작합니다.
