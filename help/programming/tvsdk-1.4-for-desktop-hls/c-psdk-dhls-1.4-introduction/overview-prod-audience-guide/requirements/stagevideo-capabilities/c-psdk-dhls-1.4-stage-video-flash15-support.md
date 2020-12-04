---
description: Flash 15 이상에서 StageVideo를 사용한 하드웨어 렌더링을 사용할 수 없을 때 StageVideo는 소프트웨어 StageVideo 개체로 원활하게 돌아갑니다.
seo-description: Flash 15 이상에서 StageVideo를 사용한 하드웨어 렌더링을 사용할 수 없을 때 StageVideo는 소프트웨어 StageVideo 개체로 원활하게 돌아갑니다.
seo-title: StageVideo에 대한 Flash 15 지원
title: StageVideo에 대한 Flash 15 지원
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# StageVideo에 대한 Flash 15 지원{#flash-support-for-stagevideo}

Flash 15 이상에서 StageVideo를 사용한 하드웨어 렌더링을 사용할 수 없을 때 StageVideo는 소프트웨어 StageVideo 개체로 원활하게 돌아갑니다.

15 StageVideo Flash에 대한 다음 정보를 고려하십시오.

* 애플리케이션에 코드를 변경할 필요가 없습니다.
* TVSDK를 변경할 필요가 없습니다.

   StageVideo를 소프트웨어에 대비하려면 TVSDK 업데이트가 필요하지 않습니다.
* Flash 15를 위해 애플리케이션을 다시 컴파일해야 합니다.
* Flash 15용으로 다시 컴파일하는 애플리케이션은 Flash 14 및 이전 버전에서 계속 작동하지만, 이러한 응용 프로그램이 Flash Player 15에서 도입된 새로운 API를 사용하지 않는 한 계속 작동합니다.

   Flash 14 응용 프로그램이 새로운 Flash 15 API를 사용해야 하는 경우 런타임 시 애플리케이션이 Flash Player 14에서 실패하지 않도록 개체 유형에 대한 캐스팅이 포함된 API를 동적으로 호출해야 합니다.

## HTML 오버레이 {#html-overlays}

Flash 15 이상에서는 하드웨어 StageVideo를 사용할 수 없게 되고 소프트웨어 StageVideo로 다시 돌아오면 HTML 오버레이를 매끄럽게 표시할 수 있습니다. 이 기능을 활성화하려면 `wmode=opaque`을(를) 설정합니다.

일부 이전 브라우저는 하드웨어 가속을 지원하지 않습니다. 이러한 요구 사항에 대한 자세한 내용은 [StageVideo 최소 요구 사항](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)을 참조하십시오. `wmode=opaque`을 설정하면 비디오가 소프트웨어 StageVideo로 렌더링되므로 성능에 영향을 줄 수 있습니다. 일반적으로 `wmode=direct`을(를) 설정하면 비디오가 GPU에 직접 렌더링되므로 성능이 훨씬 좋습니다. 그러나 이 옵션은 HTML 오버레이도 무시합니다.
