---
description: MediaPlayer 보기를 사용하여 비디오를 재생한 후, TVSDK 메서드를 사용하거나 수동으로 비디오를 숨기고 다시 표시할 수 있습니다.
title: 비디오 보기 숨기기
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 비디오 보기 숨기기{#hide-a-video-view}

MediaPlayer 보기를 사용하여 비디오를 재생한 후, TVSDK 메서드를 사용하거나 수동으로 비디오를 숨기고 다시 표시할 수 있습니다.

비디오를 지우거나 디스플레이에서 이동하기 전에 비디오를 일시 중지해야 합니다.
* 옵션 1: 다음을 사용하여 비디오 프레임 지우기 `MediaPlayer.clearVideo`나중에 &#x200B; 프레임을 바꿉니다.
   * 숨기려는 비디오를 일시 중지합니다.
   * 를 호출하여 표시된 비디오 프레임을 제거합니다. `MediaPlayer.clearVideo`.
   * 를 재설정하려면 `MediaPlayer` 다시 재생할 수 있도록, 호출 `replaceCurrentResource` 또는 `replaceCurrentItem`.
* 옵션 2: 이동 `MediaPlayer` 화면을 벗어났다가 나중에 교체하지 않고도 다시 이동할 수 있습니다.
   * 숨기려는 비디오를 일시 중지합니다.
   * 뷰를 스테이지 밖으로 이동합니다. 예:

     ```
     view.x = -300; 
     view.y = -300;
     ```

   * 비디오를 다시 표시하려면 보기를 다시 스테이지로 이동합니다.
