---
title: 최소 클라이언트 버전
description: 최소 클라이언트 버전
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# 최소 클라이언트 버전 {#minimum-client-version}

Adobe Primetime DRM 2.0.2 이상에서는 Primetime DRM 2.0 클라이언트가 인식하지 못하는 일부 새로운 사용 규칙을 소개합니다. 라이센스 서버는 지원되는 최소 클라이언트 버전( `HandlerConfiguration.setMinSupportedClientVersion()`)을 설정하여 이전 클라이언트가 이러한 사용 규칙에 대한 라이센스를 만나면 어떻게 행동하는지를 제어할 수 있습니다. 이 설정을 기반으로, 서버는 이전 클라이언트가 이해하지 못하는 사용 규칙을 무시할 수 있는지 또는 이전 클라이언트가 이러한 사용 규칙과 함께 라이센스를 사용할 수 없는지 여부를 나타낼 수 있습니다.

예를 들어

* 라이선스가 디바이스 기능 요구 사항([보호된 콘텐츠를 재생하는 데 필요한 장치 기능](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md))을 지정하는 경우 Primetime DRM 클라이언트 2.0.2 이상 버전이 이러한 요구 사항을 적용할 수 있습니다.
* 라이센스 서버가 장치 기능 요구 사항을 이해하지 못하는 클라이언트에서 내용을 재생하지 못하게 하려면 지원되는 최소 클라이언트 버전을 2(2.0.2용)로 설정합니다. 따라서 서버가 2.0.2 전에 Primetime DRM 클라이언트에 라이선스를 부여하지 못합니다. 라이센스가 한 클라이언트에서 다른 클라이언트로 전송되는 경우에도 최소 클라이언트 버전이 적용됩니다.
* 라이선스 서버에서 이전 클라이언트가 장치 기능 요구 사항을 무시하도록 허용하려는 경우 지원되는 최소 클라이언트 버전을 1(Primetime DRM 2.0의 경우)으로 설정합니다. 그런 다음 서버는 모든 클라이언트 버전 2.0 이상에 대한 라이센스를 발행합니다. 클라이언트가 버전 2.0.2 이상을 사용하여 라이센스를 다른 클라이언트로 업그레이드하거나 전송하는 경우 클라이언트가 해당 사용 규칙을 지원할 수 있으므로 라이센스의 디바이스 기능 요구 사항이 적용됩니다.

