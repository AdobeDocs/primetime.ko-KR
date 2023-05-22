---
description: ExpressPlay에서 제공하는 Primetime DRM Cloud를 사용하여 TVSDK 앱에 대한 여러 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 Apple의 FairPlay, Google의 Widevine, Microsoft의 PlayReady 및 Adobe의 Primetime Access가 포함됩니다.
title: 다중 DRM 개요
exl-id: 27614bb6-bfa6-445a-8fb5-a1b8af080bcc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 다중 DRM 워크플로우 {#multi-drm-workflows}

ExpressPlay에서 제공하는 Primetime DRM Cloud를 사용하여 TVSDK 앱에 대한 여러 DRM 솔루션을 구현할 수 있습니다. DRM 솔루션에는 Apple의 FairPlay, Google의 Widevine, Microsoft의 PlayReady 및 Adobe의 Primetime Access가 포함됩니다.

## 다중 DRM 개요 {#multi-drm-overview}

Adobe TVSDK는 여러 DRM 스키마를 사용하는 DRM 보호를 지원합니다. Adobe 오퍼 *ExpressPlay 기반의 Primetime DRM Cloud* 여러 플랫폼에서 비디오 컨텐츠의 패키징, 라이센싱 및 재생을 제공합니다.

지원되는 DRM 체계에는 Adobe의 *Primetime 액세스* DRM(AAXS)뿐만 아니라 다음을 포함한 다양한 장치의 네이티브 DRM [와이드빈](https://www.widevine.com) Chrome 및 Android에서 [페어플레이](https://developer.apple.com/streaming/fps/) Safari 및 iOS에서 [PlayReady](https://www.microsoft.com/playready/) Edge와 XboxOne에서. 이러한 플랫폼에서 현재 사용할 수 있는 DRM 스키마와 향후 릴리스의 예약 날짜에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

TVSDK는 이러한 프로토콜을 사용하여 모든 라이선스 서버에서 발급한 DRM 라이선스를 지원합니다. 여러 DRM 솔루션 지원 외에도 Adobe 오퍼는 *ExpressPlay 기반의 Primetime DRM Cloud* ExpressPlay가 각 솔루션에 대해 라이센스 서버를 운영하는 솔루션입니다. 이렇게 하면 DRM 라이센스 발급 요구 사항에 대한 설정 및 유지 관리를 간소화할 수 있습니다.

사용 *ExpressPlay 기반의 Primetime DRM Cloud* tvsdk 앱에서 DRM 요구 사항을 구현하려면 먼저 [ExpressPlay.com](https://www.expressplay.com) 계정입니다. ExpressPlay는 여러 가지 다양한 DRM 보호 체계에 대한 라이센스 기능을 제공하며 패키징 및 키 관리를 포함한 다른 서비스도 제공합니다.

귀하의 Adobe 담당자는 처음에 ExpressPlay 계정을 설정합니다. 그런 다음 계정을 구성하고 다음을 얻을 수 있습니다. *고객 인증자* ExpressPlay 서버에 대한 라이선스 토큰 요청에 사용합니다.
