---
description: Flash 15 이상부터 StageVideo를 사용한 하드웨어 렌더링을 사용할 수 없는 경우 StageVideo는 소프트웨어 StageVideo 개체로 원활하게 돌아갑니다.
title: StageVideo에 대한 Flash 15 지원
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# StageVideo에 대한 Flash 15 지원{#flash-support-for-stagevideo}

Flash 15 이상부터 StageVideo를 사용한 하드웨어 렌더링을 사용할 수 없는 경우 StageVideo는 소프트웨어 StageVideo 개체로 원활하게 돌아갑니다.

소프트웨어에 대한 Flash 15 StageVideo 폴백에 대한 다음 정보를 고려하십시오.

* 응용 프로그램에서 코드를 변경할 필요가 없습니다.
* TVSDK를 변경할 필요가 없습니다.

   StageVideo에서 소프트웨어로 폴백을 사용하기 위해 TVSDK 업데이트가 필요하지 않습니다.
* Flash 15에 대해 응용 프로그램을 다시 컴파일해야 합니다.
* Flash 15에 대해 다시 컴파일하는 애플리케이션은 이들 애플리케이션이 Flash 15에 도입된 새로운 API를 사용하지 않는 한 Flash Player 14 및 이전 버전에서 계속 작동합니다.

   Flash 14 응용 프로그램에서 새 Flash 15 API를 사용해야 하는 경우 런타임에 Flash Player 14에서 응용 프로그램이 실패하지 않도록 개체 유형에 대한 캐스팅으로 API를 동적으로 호출해야 합니다.

## HTML 오버레이 {#html-overlays}

Flash 15 이상에서는 하드웨어 StageVideo를 사용할 수 없게 되고 소프트웨어 StageVideo로 폴백되는 경우 HTML 오버레이를 원활하게 표시할 수 있습니다. 이 기능을 사용하려면 을 설정합니다. `wmode=opaque`.

일부 이전 브라우저는 하드웨어 가속을 지원하지 않습니다. 이러한 요구 사항에 대한 자세한 내용은 [StageVideo 최소 요구 사항](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). 설정 시 `wmode=opaque`, 비디오는 성능에 영향을 줄 수 있는 소프트웨어 StageVideo로 렌더링됩니다. 일반적으로 설정 `wmode=direct` 비디오를 GPU로 직접 렌더링하므로 성능이 훨씬 향상됩니다. 그러나 이 옵션은 HTML 오버레이도 무시합니다.
