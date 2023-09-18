---
description: 이 안내서에서는 Java로 구현된 Android용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
title: 제품 개요, 대상 및 이 안내서
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 제품 개요, 대상 및 이 안내서 {#product-overview-audience-and-this-guide}

이 안내서에서는 Java로 구현된 Android용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* TVSDK에서 지원하는 기능 목록은 을 참조하십시오. [Primetime TVSDK 기능](../../tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-of-the-player.md).
* TVSDK 사용을 위한 특정 하드웨어 및 소프트웨어 요구 사항에 대해서는 다음을 참조하십시오. [요구 사항](../../tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md).
* 사용 가능한 API 목록은 다음을 참조하십시오. [TVSDK Android API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/).

## 제품 개요 {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK에는 고급 비디오 기능, 콘텐츠 보호 및 광고 기능을 플레이어에 통합하는 데 도움이 되는 API 설명 및 코드 샘플이 포함되어 있습니다. Java를 사용하여 비디오 플레이어 사용자 인터페이스를 만듭니다. TVSDK를 사용하면 해당 사용자 인터페이스를 미디어 플레이어에 연결할 수 있습니다. 미디어 매니페스트를 기반으로 비디오 및 광고를 재생할 수 있습니다. TVSDK를 사용하여 비디오에 대한 정보를 검색하고 보안을 처리하며 재생을 제어하고 모니터링할 수도 있습니다.

## 대상자 {#section_527860B373734D3BA89FCF5EC1F6DC37}

이 안내서에서는 Java를 사용하여 애플리케이션 및 비디오 플레이어를 개발하는 방법을 알고 있다고 가정합니다. 비디오 플레이어 UI를 Java로 구현하고 필요한 TVSDK 기능을 통합합니다.

## 이 안내서 정보 {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

이 안내서에서는 Android 장치에서 Java를 사용하여 비디오 플레이어에서 TVSDK 기능을 통합할 수 있는 정보를 제공합니다.

## 이 안내서의 네임스페이스 표기법 {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>TVSDK API 네임스페이스 접두사 [!DNL com.adobe.mediacore] 은 간결성을 위해 생략되는 경우가 많습니다.
>
>컨텍스트가 명확하면 상위 클래스 지정자 없이 많은 API 요소가 참조됩니다.
