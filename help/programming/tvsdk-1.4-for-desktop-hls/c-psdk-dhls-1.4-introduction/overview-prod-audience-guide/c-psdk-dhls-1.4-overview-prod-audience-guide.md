---
description: 이 안내서에서는 ActionScript에서 구현된 데스크톱 HLS용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
title: 개요
exl-id: 02efcef8-c4ac-4ff9-bf3b-4ca6553f7617
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 개요 {#overview}

이 안내서에서는 ActionScript에서 구현된 데스크톱 HLS용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.

## 제품 개요 {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK에는 고급 비디오 기능, 콘텐츠 보호 및 광고 기능을 플레이어에 통합하는 데 도움이 되는 API 설명 및 코드 샘플이 포함되어 있습니다. ActionScript을 사용하여 비디오 플레이어 사용자 인터페이스를 만듭니다. TVSDK를 사용하면 해당 사용자 인터페이스를 미디어 플레이어에 연결할 수 있습니다. 미디어 매니페스트를 기반으로 비디오 및 광고를 재생할 수 있습니다. TVSDK를 사용하여 비디오에 대한 정보를 검색하고 보안을 처리하며 재생을 제어하고 모니터링할 수도 있습니다.

TVSDK 사용을 위한 특정 하드웨어 및 소프트웨어 요구 사항에 대해서는 다음을 참조하십시오. [요구 사항](../../c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/r-psdk-dhls-1.4-requirements-system.md).

## 대상자 {#section_527860B373734D3BA89FCF5EC1F6DC37}

이 안내서에서는 사용자가 ActionScript을 사용하여 응용 프로그램 및 비디오 플레이어를 개발하는 방법을 알고 있다고 가정합니다. 해당 언어를 사용하여 비디오 플레이어 사용자 인터페이스를 구현하고 TVSDK 기능을 통합합니다.

## 이 안내서 정보 {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

이 안내서에서는 데스크톱 컴퓨터에서 ActionScript을 사용하여 비디오 플레이어에서 TVSDK 기능을 통합할 수 있는 정보를 제공합니다.

## 이 안내서의 네임스페이스 표기법 {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>TVSDK API 네임스페이스 접두사 `com.adobe.mediacore` 은 간결성을 위해 생략됩니다.
>
>컨텍스트가 명확하면 상위 클래스 지정자 없이 많은 API 요소가 참조됩니다.
