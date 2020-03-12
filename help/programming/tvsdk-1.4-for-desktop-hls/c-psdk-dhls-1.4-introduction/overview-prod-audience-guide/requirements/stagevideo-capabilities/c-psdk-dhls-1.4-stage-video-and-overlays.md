---
description: StageVideo와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 StageVideo 평면 위에 있으므로 StageVideo는 항상 모든 Flash 표시 목록 요소 뒤에 표시됩니다.
seo-description: StageVideo와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 StageVideo 평면 위에 있으므로 StageVideo는 항상 모든 Flash 표시 목록 요소 뒤에 표시됩니다.
seo-title: 스테이지 비디오 및 HTML 오버레이
title: 스테이지 비디오 및 HTML 오버레이
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 스테이지 비디오 및 HTML 오버레이{#stagevideo-and-html-overlays}

StageVideo와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 StageVideo 평면 위에 있으므로 StageVideo는 항상 모든 Flash 표시 목록 요소 뒤에 표시됩니다.

HTML 오버레이는 자체 평면으로 렌더링되는 비디오의 Flash 디스플레이 평면에 표시할 수 `StageVideo` 있는 UI 요소입니다. Flash 15 이전에는 하드웨어 가속을 사용할 수 없을 때 HTML 오버레이를 사용할 수 없었습니다. Flash 15부터 HTML 오버레이는 소프트웨어 렌더링으로 `StageVideo` 돌아올 때 표시됩니다.

>[!IMPORTANT]
>
>시스템의 기능에 따라 HTML 오버레이를 사용할 때 성능이 크게 또는 약간 저하될 수 있습니다.

다음 정보를 고려하십시오.

* Flash Player 15:

   * 하드웨어 가속을 사용할 수 있는지 여부에 관계없이 HTML 오버레이를 사용할 수 있습니다.
   * HTML 오버레이를 사용하려면 로 `wmode` 설정합니다 `opaque`.

* Flash Player 14:

   * 하드웨어 가속을 사용할 수 있는 경우 Flash 디스플레이 목록 아래에 `StageVideo` 있으므로 HTML 오버레이를 사용할 수 있습니다.
   * 하드웨어 가속을 사용할 수 없는 경우 비디오는 브라우저의 다른 모든 요소 위에 렌더링되므로 HTML 오버레이를 사용할 수 없습니다.

다음은 HTML 오버레이를 사용하기 위한 최소 브라우저 요구 `StageVideo`사항입니다.

* Firefox 버전 4 이상
* Safari 버전 4 이상
* Internet Explorer:

   * Windows 7 이상의 경우 버전 9+
   * Windows XP의 버전 10+

* Chrome 버전 26 이상

   >[!IMPORTANT]
   >
   >Windows XP 및 Windows Vista에서 Chrome Pepper는 지원되지 않습니다.

