---
description: ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.
title: ConfigProvider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.

[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 클래스를 사용하여 `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` 및 `IQosConfig` 구성 인터페이스를 구현하면 기능 관리자가 구성을 읽을 수 있습니다. 예를 들어 `ICCConfig`은 `CCManager` 구성을 위한 인터페이스입니다. 구성 파일은 JSON 구성 파일에서 구성 매개 변수를 받습니다.

`ConfigProvider.java` 파일은 Adobe이 구성 인터페이스를 구현한 예입니다. 구성이 저장되는 `SharedPreferences`의 설정을 읽습니다. 조직에 적합한 방식으로 구성을 저장할 수 있습니다. 구성 구현은 구성 소스의 래퍼를 제공합니다.