---
description: 이 안내서에서는 ActionScript에서 구현되는 데스크탑 HLS용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.
title: 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 개요 {#overview}

이 안내서에서는 ActionScript에서 구현되는 데스크탑 HLS용 TVSDK를 사용하여 비디오 플레이어 애플리케이션을 개발하는 방법에 대한 정보를 제공합니다.

## 제품 개요 {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK에는 고급 비디오 기능, 컨텐츠 보호 및 광고 기능을 플레이어에 통합하는 데 도움이 되는 API 설명 및 코드 샘플이 포함되어 있습니다. ActionScript을 사용하여 비디오 플레이어 사용자 인터페이스를 만듭니다. TVSDK를 사용하면 해당 유저 인터페이스를 미디어 플레이어에 연결할 수 있습니다. 미디어 매니페스트를 기반으로 비디오와 광고를 재생할 수 있습니다. 또한 TV SDK를 사용하여 비디오 정보를 검색하고 보안을 처리하며 재생을 제어하고 모니터링할 수 있습니다.

TVSDK 사용에 대한 특정 하드웨어 및 소프트웨어 요구 사항은 [요구 사항](../../c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/r-psdk-dhls-1.4-requirements-system.md)을 참조하십시오.

## 대상 {#section_527860B373734D3BA89FCF5EC1F6DC37}

이 안내서에서는 ActionScript을 사용하여 응용 프로그램 및 비디오 플레이어를 개발하는 방법을 이해한다고 가정합니다. 해당 언어를 사용하고 TVSDK 기능을 통합하여 비디오 플레이어 사용자 인터페이스를 구현합니다.

## 이 안내서 {#section_9A5B2FC506B34B5DB71CA827B307A4D0} 정보

이 안내서에서는 데스크톱 컴퓨터의 ActionScript을 사용하여 비디오 플레이어에 TVSDK 기능을 통합할 수 있도록 하는 정보를 제공합니다.

## 이 안내서의 네임스페이스 표기법{#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>TVSDK API 네임스페이스 접두어 `com.adobe.mediacore`은(는) 간결하게 생략되었습니다.
>
>컨텍스트가 명확하면 상위 클래스 지정자가 없는 많은 API 요소를 참조합니다.

