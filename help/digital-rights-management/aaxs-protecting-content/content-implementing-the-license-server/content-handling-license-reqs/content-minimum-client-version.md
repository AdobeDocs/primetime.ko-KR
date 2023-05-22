---
title: 최소 클라이언트 버전
description: 최소 클라이언트 버전
copied-description: true
exl-id: ba311d33-f3dd-42c5-ac66-7ad665d1bd20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 최소 클라이언트 버전 {#minimum-client-version}

Adobe 액세스 2.0.2 이상에서는 Adobe 액세스 2.0 클라이언트가 인식하지 못하는 몇 가지 새로운 사용 규칙을 도입합니다. 지원되는 최소 클라이언트 버전( `HandlerConfiguration.setMinSupportedClientVersion()`) 라이선스 서버는 오래된 클라이언트가 이러한 사용 규칙에 따라 라이선스를 받을 때 어떻게 동작할지 제어할 수 있습니다. 이 설정을 기반으로 서버는 이전 클라이언트가 이해할 수 없는 사용 규칙을 무시할 수 있는지 여부 또는 이전 클라이언트가 이러한 사용 규칙으로 라이선스를 사용할 수 없는지 여부를 나타낼 수 있습니다.

예를 들어,

* 라이센스에서 디바이스 기능 요구 사항( [보호된 콘텐츠를 재생하는 데 필요한 장치 기능](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), Adobe 액세스 클라이언트 2.0.2 이상은 이러한 요구 사항을 적용할 수 있습니다.
* 라이센스 서버가 디바이스 기능 요구 사항 을 이해하지 못하는 클라이언트에서 컨텐츠를 재생하지 않도록 하려면 지원되는 최소 클라이언트 버전을 2(2.0.2의 경우)로 설정하십시오. 이렇게 하면 서버가 2.0.2 이전에 Adobe 액세스 클라이언트에 라이선스를 발급할 수 없습니다. 라이센스가 한 클라이언트에서 다른 클라이언트로 전송되는 경우 최소 클라이언트 버전도 적용됩니다.
* 라이센스 서버에서 이전 클라이언트가 장치 기능 요구 사항을 무시하도록 허용하려면 지원되는 최소 클라이언트 버전을 1로 설정합니다(Adobe 액세스 2.0의 경우). 서버가 모든 클라이언트 버전 2.0 이상에 라이선스를 발급합니다. 클라이언트가 버전 2.0.2 이상의 다른 클라이언트로 라이센스를 업그레이드하거나 전송하는 경우 클라이언트는 이제 해당 사용 규칙을 지원하므로 라이센스의 장치 기능 요구 사항이 적용됩니다.
