---
description: StageVideo에서 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 StageVideo 평면 위에 있으므로 StageVideo는 항상 모든 Flash 표시 목록 요소 뒤에 표시됩니다.
title: StageVideo 및 HTML 오버레이
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo 및 HTML 오버레이{#stagevideo-and-html-overlays}

StageVideo에서 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 StageVideo 평면 위에 있으므로 StageVideo는 항상 모든 Flash 표시 목록 요소 뒤에 표시됩니다.

HTML 오버레이는 다음에 의해 렌더링되는 비디오에서 Flash 표시 평면에 표시할 수 있는 UI 요소입니다 `StageVideo` 전용기에요. Flash 15 이전에는 하드웨어 가속을 사용할 수 없는 경우 HTML 오버레이를 사용할 수 없었습니다. Flash 15부터 다음과 같은 경우 HTML 오버레이가 표시됩니다. `StageVideo` 소프트웨어 렌더링으로 돌아갑니다.

>[!IMPORTANT]
>
>시스템의 기능에 따라 HTML 오버레이를 사용할 때 성능이 저하되거나 저하될 수 있습니다.

다음 정보를 고려하십시오.

* Flash Player 15에서:

   * 하드웨어 가속을 사용할 수 있는지 여부에 관계없이 HTML 오버레이를 사용할 수 있습니다.
   * HTML 오버레이를 사용하려면 을 설정합니다 `wmode` 끝 `opaque`.

* Flash Player 14에서:

   * 하드웨어 가속을 사용할 수 있는 경우 `StageVideo` 은 Flash 표시 목록 아래에 있으므로 HTML 오버레이를 사용할 수 있습니다.
   * 하드웨어 가속을 사용할 수 없는 경우 브라우저의 다른 모든 요소 위에 비디오가 렌더링되므로 HTML 오버레이를 사용할 수 없습니다.

다음은 HTML 오버레이를 사용할 최소 브라우저 요구 사항입니다 `StageVideo`:

* Firefox 버전 4 이상
* Safari 버전 4 이상
* Internet Explorer:

   * Windows 7 이상 버전 9+
   * Windows XP의 버전 10 이상

* Chrome 버전 26 이상

   >[!IMPORTANT]
   >
   >Windows XP 및 Windows Vista의 Chrome Pepper는 지원되지 않습니다.
