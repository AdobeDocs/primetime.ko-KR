---
description: ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

ConfigProvider 클래스는 미디어 플레이어에 대한 구성을 가져옵니다. 기능 관리자가 구성 정보를 읽을 수 있도록 구성 인터페이스를 구현해야 합니다.

다음을 사용합니다. [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 을 구현할 클래스 `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, 및 `IQosConfig` 기능 관리자가 구성을 읽을 수 있도록 구성 인터페이스를 제공합니다. 예를 들어 `ICCConfig` 은(는) 의 인터페이스입니다. `CCManager` 구성. 구성 파일은 JSON 구성 파일에서 구성 매개 변수를 수신합니다.

다음 `ConfigProvider.java` 파일은 Adobe이 구성 인터페이스를 구현하는 예제입니다. 다음에서 설정을 읽습니다. `SharedPreferences`: 구성이 저장되는 위치입니다. 조직에 적합한 방식으로 구성을 저장할 수 있습니다. 구성 구현은 구성 소스에 대한 래퍼를 제공합니다.
