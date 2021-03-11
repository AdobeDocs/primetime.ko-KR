---
description: 비디오를 재생하는 데 MediaPlayer 보기가 사용된 후 TV SDK 메서드를 사용하거나 수동으로 표시하여 비디오를 숨기고 다시 표시할 수 있습니다.
title: 비디오 보기 숨기기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 비디오 보기 숨기기{#hide-a-video-view}

비디오를 재생하는 데 MediaPlayer 보기가 사용된 후 TV SDK 메서드를 사용하거나 수동으로 표시하여 비디오를 숨기고 다시 표시할 수 있습니다.

비디오를 지우거나 디스플레이에서 이동하려면 먼저 비디오를 일시 중지해야 합니다.
* 옵션 1:비디오 프레임을 `MediaPlayer.clearVideo`으로 지우고 나중에 &#x200B; 프레임을 바꿉니다.
   * 숨길 비디오를 일시 중지합니다.
   * `MediaPlayer.clearVideo`을(를) 호출하여 표시된 비디오 프레임을 제거합니다.
   * 다시 재생할 수 있도록 `MediaPlayer`을 다시 설정하려면 `replaceCurrentResource` 또는 `replaceCurrentItem`로 전화하십시오.
* 옵션 2:`MediaPlayer` 보기를 화면에서 이동하여 나중에 교체하지 않고 다시 이동합니다.
   * 숨길 비디오를 일시 중지합니다.
   * 보기를 스테이지 밖으로 이동합니다. 예:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 비디오를 다시 표시하려면 보기를 스테이지로 다시 이동합니다.
