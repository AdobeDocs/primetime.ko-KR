---
description: 'null'
seo-description: 'null'
seo-title: 보호된 콘텐츠를 재생할 수 있는 Primetime DRM 애플리케이션 목록 허용
title: 보호된 콘텐츠를 재생할 수 있는 Primetime DRM 애플리케이션 목록 허용
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# 보호된 콘텐츠를 재생할 수 있는 Primetime DRM 애플리케이션 목록 허용{#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

허용 목록은 컨텐츠를 재생할 수 있는 AIR, iOS 및 Android 애플리케이션을 지정합니다. 또한 AIR 및 iOS 응용 프로그램 ID, 최소 버전, 최대 버전 및 게시자 ID를 지정합니다.

사용 사례 예: 이 규칙을 사용하여 특정 응용 프로그램의 재생을 제한하거나 콘텐트에 액세스할 수 있는 응용 프로그램 버전을 제어할 수 있습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Flash Builder를 사용하여 보호된 애플리케이션을 빌드하는 경우 디버그 모드에서 애플리케이션을 배포하지 않아야 합니다. 디버그 모드에서 응용 프로그램을 배포하면 Flash Builder가 AIR 응용 프로그램 ID `.debug` 에 추가되어 Primetime DRM의 허용 목록 기능이 예기치 않게 동작합니다.

