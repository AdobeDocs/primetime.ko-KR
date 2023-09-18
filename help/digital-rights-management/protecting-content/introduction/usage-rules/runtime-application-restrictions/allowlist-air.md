---
title: 보호된 컨텐츠 재생이 허용된 Primetime DRM 애플리케이션에 대한 허용 목록
description: 보호된 컨텐츠 재생이 허용된 Primetime DRM 애플리케이션에 대한 허용 목록
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 보호된 컨텐츠 재생이 허용된 Primetime DRM 애플리케이션에 대한 허용 목록 {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

허용 목록은 컨텐츠 재생이 허용되는 AIR, iOS 및 Android 애플리케이션을 지정합니다. 또한 AIR 및 iOS 애플리케이션 ID, 최소 버전, 최대 버전 및 게시자 ID를 지정합니다.

예제 사용 사례: 이 규칙을 사용하여 재생을 특정 애플리케이션으로 제한하거나 콘텐츠에 액세스할 수 있는 애플리케이션 버전을 제어합니다.

>[!NOTE]
>
>Adobe Flash Builder을 사용하여 보호된 응용 프로그램을 빌드하는 경우 디버그 모드에서 응용 프로그램을 배포하지 않도록 해야 합니다. 디버그 모드에서 응용 프로그램을 배포하면 Flash Builder이 추가됩니다 `.debug` Primetime DRM의 허용 목록 기능이 예기치 않게 작동하는 AIR 애플리케이션 ID에 대해 설명합니다.
