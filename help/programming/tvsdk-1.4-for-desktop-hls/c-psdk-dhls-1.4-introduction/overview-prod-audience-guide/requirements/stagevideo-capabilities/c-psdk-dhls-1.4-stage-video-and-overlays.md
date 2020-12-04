---
description: 스테이지 비디오와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 스테이지 비디오 평면 위에 있으므로 StageVideo는 항상 Flash 표시 목록 요소 뒤에 표시됩니다.
seo-description: 스테이지 비디오와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 스테이지 비디오 평면 위에 있으므로 StageVideo는 항상 Flash 표시 목록 요소 뒤에 표시됩니다.
seo-title: 스테이지 비디오 및 HTML 오버레이
title: 스테이지 비디오 및 HTML 오버레이
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 스테이지 비디오 및 HTML 오버레이{#stagevideo-and-html-overlays}

스테이지 비디오와 함께 HTML 오버레이를 사용하여 Flash 표시 목록 비디오 평면에 UI 요소를 표시할 수 있습니다. 이 평면은 스테이지 비디오 평면 위에 있으므로 StageVideo는 항상 Flash 표시 목록 요소 뒤에 표시됩니다.

HTML 오버레이는 자체 평면에서 `StageVideo`에 의해 렌더링되는 비디오의 Flash 표시 평면에 표시할 수 있는 UI 요소입니다. Flash 15 이전에는 하드웨어 가속을 사용할 수 없을 때 HTML 오버레이를 사용할 수 없었습니다. Flash 15부터 HTML 오버레이는 `StageVideo`이(가) 소프트웨어 렌더링으로 돌아올 때 표시됩니다.

>[!IMPORTANT]
>
>시스템의 기능에 따라 HTML 오버레이를 사용할 때 성능이 더 크거나 작아 저하될 수 있습니다.

다음 정보를 고려하십시오.

* Flash Player 15:

   * 하드웨어 가속을 사용할 수 있는지 여부를 HTML 오버레이를 사용할 수 있습니다.
   * HTML 오버레이를 사용하려면 `wmode`을(를) `opaque`(으)로 설정합니다.

* Flash Player 14:

   * 하드웨어 가속을 사용할 수 있는 경우, `StageVideo`은 Flash 표시 목록 아래에 있으므로 HTML 오버레이를 사용할 수 있습니다.
   * 하드웨어 가속을 사용할 수 없는 경우 비디오는 브라우저의 모든 다른 요소 위에 렌더링되므로 HTML 오버레이를 사용할 수 없습니다.

다음은 `StageVideo`과 함께 HTML 오버레이를 사용하기 위한 최소 브라우저 요구 사항입니다.

* Firefox 버전 4 이상
* Safari 버전 4 이상
* Internet Explorer:

   * Windows 7 이상의 경우 버전 9+
   * Windows XP 기반의 버전 10+

* Chrome 버전 26 이상

   >[!IMPORTANT]
   >
   >Windows XP 및 Windows Vista에서 Chrome Pepper는 지원되지 않습니다.

