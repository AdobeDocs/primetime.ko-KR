---
description: 사용자 지정 스킨을 사용하려면 default-video-controls.css와 유사한 사용자 지정을 작성하고 플레이어에서 이 새로운 사용자 지정을 참조해야 합니다.
title: 사용자 정의 스킨
exl-id: 4d627545-942d-4883-a010-afddcffb8dd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 사용자 정의 스킨{#custom-skins}

사용자 지정 스킨을 사용하려면 default-video-controls.css와 유사한 사용자 지정을 작성하고 플레이어에서 이 새로운 사용자 지정을 참조해야 합니다.

예를 들어 다음 옵션 중 하나를 사용할 수 있습니다.

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

다음과 같은 유형을 변경할 수 있습니다.

* 단추 및 텍스트의 전경색

   전경이 있는 모든 컨트롤에서 `vid-skin-fgcolor` 클래스. 모든 컨트롤의 전경색을 변경하려면 `vid-skin-fgcolor` 을(를) 분류하고 원하는 색상을 지정합니다.
* 단추 및 텍스트의 배경색

   전경이 있는 모든 컨트롤에서 `vid-skin-bgcolor` 클래스. 모든 컨트롤의 전경을 변경하려면 다음을 사용하여 모든 요소를 반복합니다. `vid-skin-bgcolor` 을(를) 분류하고 원하는 색상을 지정합니다.
* 재생 헤드 모양

   플레이헤드는 사각형이거나 둥글게 만들 수 있습니다. 재생 헤드를 변경하려면 를 추가합니다. `square` 또는 `round` 클래스 대상 `playhead` 요소를 생성하지 않습니다.
* 버퍼링 스피너의 스타일

   참조 플레이어는 플레이어가 콘텐츠를 버퍼링할 때 표시할 수 있는 다음과 같은 스타일의 스피너를 제공합니다.

   * 오버레이 텍스트( `overlay-text`)
   * 사각형 회전기( `spinner`)
   * 신호 ( `signal`)
   * 세로 막대( `vertical`)

      >[!TIP]
      >
      >버퍼링 스피너를 사용하려면 버퍼링 오버레이 요소에 클래스를 추가해야 합니다. 예를 들어, `overlay-text`에 다음 줄을 추가합니다. `BufferOverlay.js` 파일:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```
