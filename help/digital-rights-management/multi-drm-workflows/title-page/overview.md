---
description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 대한 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 Apple의 FairPlay, Google의 Widevine, Microsoft의 PlayReady, Adobe의 Primetime Access 등이 포함되어 있습니다.
seo-description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 대한 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 Apple의 FairPlay, Google의 Widevine, Microsoft의 PlayReady, Adobe의 Primetime Access 등이 포함되어 있습니다.
seo-title: 다중 DRM 개요
title: 다중 DRM 개요
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 다중 DRM 워크플로우 {#multi-drm-workflows}

ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 대한 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 Apple의 FairPlay, Google의 Widevine, Microsoft의 PlayReady, Adobe의 Primetime Access 등이 포함되어 있습니다.

## 다중 DRM 개요 {#multi-drm-overview}

Adobe TVSDK 파섹 Adobe는 *ExpressPlay를* 기반으로 다양한 플랫폼에서 동영상 콘텐츠를 패키징, 라이선스 및 재생할 수 있는 Primetime DRM Cloud를 제공합니다.

지원되는 DRM 체계에는 Adobe의 *Primetime* Access DRM(AAXS) [, Chrome 및 Android](https://www.widevine.com) 의 Widevine, Safari 및 iOS의 FairPlay [, Edge 및 XboxOne](https://developer.apple.com/streaming/fps/) [](https://www.microsoft.com/playready/) 의 PlayReady DRM등이 포함되어 있습니다. 이러한 플랫폼에서 현재 사용할 수 있는 DRM 구성표와 향후 릴리스의 예약된 날짜에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

TVSDK 파섹 Adobe는 다양한 DRM 솔루션을 지원할 뿐만 아니라 ExpressPlay *에서* 제공하는 솔루션으로 Primetime DRM Cloud를 제공합니다. 따라서 DRM 라이선스 발급 요구 사항에 대한 설정 및 유지 관리가 간소화됩니다.

TVSDK *앱에서 DRM 요구 사항을* 구현하기 위해 ExpressPlay 기반의 Primetime DRM Cloud를 사용하려면 먼저 ExpressPlay.com [계정을](https://www.expressplay.com) 구해야 합니다. ExpressPlay는 다양한 DRM 보호 체계를 위한 라이선스 기능을 제공하며 패키징 및 키 관리 등 다른 서비스를 제공합니다.

Adobe 담당자가 처음에 ExpressPlay 계정을 설정합니다. 그런 다음 계정을 구성하고 ExpressPlay 서버에 대한 라이센스 토큰 요청에 사용할 *고객* 인증자를 가져올 수 있습니다.