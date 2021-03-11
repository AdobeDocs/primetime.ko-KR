---
description: 사용자 정의 스킨을 사용하려면 default-video-controls.css와 유사한 사용자 정의 스킨을 작성하고 플레이어에서 이 새로운 사용자 정의 스킨을 참조해야 합니다.
title: 사용자 정의 스킨
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 사용자 정의 스킨{#custom-skins}

사용자 정의 스킨을 사용하려면 default-video-controls.css와 유사한 사용자 정의 스킨을 작성하고 플레이어에서 이 새로운 사용자 정의 스킨을 참조해야 합니다.

예를 들어 다음 옵션 중 하나를 사용할 수 있습니다.

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

다음과 같은 유형의 변경 작업을 수행할 수 있습니다.

* 단추 및 텍스트의 전경색

   전경이 있는 모든 컨트롤은 `vid-skin-fgcolor` 클래스를 사용합니다. 모든 컨트롤의 전경을 변경하려면 `vid-skin-fgcolor` 클래스를 사용하여 모든 요소를 반복하고 원하는 색상을 지정합니다.
* 단추 및 텍스트의 배경색

   전경이 있는 모든 컨트롤은 `vid-skin-bgcolor` 클래스를 사용합니다. 모든 컨트롤의 전경을 변경하려면 `vid-skin-bgcolor` 클래스를 사용하여 모든 요소를 반복하고 원하는 색상을 지정합니다.
* 재생 헤드 모양

   재생 헤드는 사각형 또는 둥글게 할 수 있다. 재생 헤드를 변경하려면 `square` 또는 `round` 클래스를 `playhead` 요소에 추가합니다.
* 버퍼링 스피너의 스타일

   참조 플레이어는 플레이어가 컨텐츠를 버퍼링할 때 다음 스피너의 스타일을 표시할 수 있도록 제공합니다.

   * 오버레이-텍스트( `overlay-text`)
   * 사각형 스피너( `spinner`)
   * 신호( `signal`)
   * 세로 막대( `vertical`)

      >[!TIP]
      >
      >버퍼링 분할자를 사용하려면 버퍼링 오버레이 요소에 클래스를 추가해야 합니다. 예를 들어 `overlay-text`을 사용하려면 `BufferOverlay.js` 파일에 다음 줄을 추가합니다.
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

