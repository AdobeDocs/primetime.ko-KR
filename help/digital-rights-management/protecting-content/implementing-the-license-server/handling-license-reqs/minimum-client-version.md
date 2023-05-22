---
title: 최소 클라이언트 버전
description: 최소 클라이언트 버전
copied-description: true
exl-id: c4aebafe-33b4-4da3-9e79-53d6a7e9f22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 최소 클라이언트 버전 {#minimum-client-version}

Adobe Primetime DRM 2.0.2 이상에서는 Primetime DRM 2.0 클라이언트가 이해하지 못하는 몇 가지 새로운 사용 규칙을 도입합니다. 지원되는 최소 클라이언트 버전( `HandlerConfiguration.setMinSupportedClientVersion()`) 라이센스 서버는 오래된 클라이언트가 이러한 사용 규칙에 따라 라이센스를 받을 때 작동하는 방식을 제어할 수 있습니다. 이 설정을 기반으로 서버는 이전 클라이언트가 이해할 수 없는 사용 규칙을 무시할 수 있는지 여부 또는 이전 클라이언트가 이러한 사용 규칙으로 라이선스를 사용할 수 없는지 여부를 나타낼 수 있습니다.

예를 들어,

* 라이센스에서 디바이스 기능 요구 사항( [보호된 콘텐츠를 재생하는 데 필요한 장치 기능](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), Primetime DRM 클라이언트 2.0.2 이상은 이러한 요구 사항을 적용할 수 있습니다.
* 라이센스 서버가 디바이스 기능 요구 사항 을 이해하지 못하는 클라이언트에서 컨텐츠를 재생하지 않도록 하려면 지원되는 최소 클라이언트 버전을 2(2.0.2의 경우)로 설정하십시오. 이렇게 하면 서버가 2.0.2 이전의 Primetime DRM 클라이언트에 라이선스를 발급할 수 없습니다. 라이센스가 한 클라이언트에서 다른 클라이언트로 전송되는 경우 최소 클라이언트 버전도 적용됩니다.
* 라이센스 서버에서 이전 클라이언트가 장치 기능 요구 사항을 무시하도록 허용하려면 지원되는 최소 클라이언트 버전을 1(Primetime DRM 2.0의 경우)로 설정합니다. 그런 다음 서버는 클라이언트 버전 2.0 이상에 라이센스를 발행합니다. 클라이언트가 버전 2.0.2 이상의 다른 클라이언트로 라이센스를 업그레이드하거나 전송하는 경우 클라이언트가 해당 사용 규칙을 지원할 수 있으므로 라이센스의 장치 기능 요구 사항이 적용됩니다.
