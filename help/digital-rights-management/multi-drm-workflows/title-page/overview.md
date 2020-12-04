---
description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 애플의 페어플레이, 구글의 와이어드인, 마이크로소프트의 플레이레디, 그리고 Adobe의 프라임타임 액세스 등이 포함됩니다.
seo-description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 애플의 페어플레이, 구글의 와이어드인, 마이크로소프트의 플레이레디, 그리고 Adobe의 프라임타임 액세스 등이 포함됩니다.
seo-title: 다중 DRM 개요
title: 다중 DRM 개요
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# 다중 DRM 워크플로 {#multi-drm-workflows}

ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 TVSDK 앱에 다양한 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 애플의 페어플레이, 구글의 와이어드인, 마이크로소프트의 플레이레디, 그리고 Adobe의 프라임타임 액세스 등이 포함됩니다.

## 다중 DRM 개요 {#multi-drm-overview}

Adobe TVSDK는 다양한 DRM 체계를 사용하여 DRM 보호를 지원합니다. Adobe은 다양한 플랫폼에서 비디오 컨텐츠의 패키징, 라이선스 및 재생을 제공하기 위해 ExpressPlay *기반의* Primetime DRM Cloud를 제공합니다.

지원되는 DRM 체계에는 Adobe *Primetime Access* DRM(AAXS)과 Chrome 및 Android의 [Widevine](https://www.widevine.com), Safari 및 iOS의 [FairPlay](https://developer.apple.com/streaming/fps/) 및 [Edge 및 XboxOne에서 playReady](https://www.microsoft.com/playready/) Adobe 담당자에게 현재 이러한 플랫폼에서 DRM 체계를 사용할 수 있는 정보와 향후 릴리스의 예정된 날짜에 대한 정보를 확인하십시오.

TVSDK는 이러한 프로토콜을 사용하여 라이센스 서버에서 발행한 DRM 라이센스를 지원합니다. Adobe은 여러 DRM 솔루션에 대한 지원 외에도 ExpressPlay가 각 솔루션에 대한 라이선스 서버를 운영하는 솔루션으로 ExpressPlay *에서 제공하는* Primetime DRM Cloud를 제공합니다. 따라서 DRM 라이선스 발급에 필요한 설정 및 유지 관리를 간소화할 수 있습니다.

TVSDK 앱에서 DRM 요구 사항을 구현하기 위해 ExpressPlay *에서 제공하는* Primetime DRM Cloud를 사용하려면 먼저 [ExpressPlay.com](https://www.expressplay.com) 계정을 구해야 합니다. ExpressPlay는 다양한 DRM 보호 체계를 위한 라이선스 기능을 제공하며 패키징 및 키 관리 등 다른 서비스를 제공합니다.

Adobe 담당자가 처음에 ExpressPlay 계정을 설정합니다. 그런 다음 계정을 구성하고 ExpressPlay 서버에 대한 라이센스 토큰 요청에 사용할 *고객 인증자*&#x200B;를 가져올 수 있습니다.