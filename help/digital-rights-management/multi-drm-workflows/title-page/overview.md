---
description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 애플의 FairPlay, 구글의 Widevin, Microsoft의 PlayReady, Adobe의 Primetime Access 등이 포함됩니다.
title: 다중 DRM 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 다중 DRM 워크플로 {#multi-drm-workflows}

ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 애플의 FairPlay, 구글의 Widevin, Microsoft의 PlayReady, Adobe의 Primetime Access 등이 포함됩니다.

## 다중 DRM 개요 {#multi-drm-overview}

Adobe TVSDK는 다양한 DRM 스킴을 사용하여 DRM 보호를 지원합니다. Adobe은 다양한 플랫폼에서 비디오 컨텐츠의 패키징, 라이선스 부여 및 재생을 제공하기 위해 ExpressPlay *기반의* Primetime DRM Cloud를 제공합니다.

지원되는 DRM 스킴에는 Adobe의 *Primetime Access* DRM(AAXS)과 Chrome 및 Android의 [Widevine](https://www.widevine.com), Safari 및 iOS의 [FairPlay](https://developer.apple.com/streaming/fps/) 및 [Drm이 포함됩니다. Edge 및 XboxOne에서 playReady](https://www.microsoft.com/playready/) 이러한 플랫폼에서 현재 사용할 수 있는 DRM 스킴과 향후 릴리스의 예약된 날짜에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

TVSDK는 이러한 프로토콜을 사용하여 라이센스 서버에서 발행한 DRM 라이센스를 지원합니다. 여러 DRM 솔루션에 대한 지원 외에도 Adobe은 ExpressPlay가 각 솔루션에 대한 라이선스 서버를 운영하는 솔루션으로 ExpressPlay *기반의* Primetime DRM Cloud를 제공합니다. 이렇게 하면 DRM 라이선스 발급에 필요한 설정 및 유지 관리를 간소화할 수 있습니다.

TVSDK 앱에서 DRM 요구 사항을 구현하기 위해 ExpressPlay *기반의* Primetime DRM Cloud를 사용하려면 먼저 [ExpressPlay.com](https://www.expressplay.com) 계정을 구해야 합니다. ExpressPlay는 다양한 DRM 보호 체계를 위한 라이선스 기능을 제공하며 패키징 및 키 관리 등 다른 서비스를 제공합니다.

Adobe 담당자가 처음에 ExpressPlay 계정을 설정합니다. 그런 다음 계정을 구성하고 ExpressPlay 서버에 대한 라이센스 토큰 요청에 사용할 *고객 인증자*&#x200B;를 가져올 수 있습니다.