---
description: ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.
seo-description: ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.

[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 클래스를 사용하여 `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` 및 `IQosConfig` 구성 인터페이스를 구현하면 기능 관리자가 구성을 읽을 수 있습니다. 예를 들어 `ICCConfig`은 `CCManager` 구성에 대한 인터페이스입니다. 구성 파일은 JSON 구성 파일에서 구성 매개 변수를 받습니다.

`ConfigProvider.java` 파일은 구성 인터페이스의 Adobe 구현의 예입니다. 구성이 저장되는 `SharedPreferences`의 설정을 읽습니다. 조직에 적합한 방식으로 구성을 저장할 수 있습니다. 구성 구현은 구성 소스에 대한 래퍼를 제공합니다.