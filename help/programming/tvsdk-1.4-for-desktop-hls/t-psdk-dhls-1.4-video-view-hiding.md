---
description: 비디오를 재생하는 데 MediaPlayer 보기가 사용된 후 TV SDK 메서드를 사용하거나 수동으로 표시하여 숨길 수 있습니다.
seo-description: 비디오를 재생하는 데 MediaPlayer 보기가 사용된 후 TV SDK 메서드를 사용하거나 수동으로 표시하여 숨길 수 있습니다.
seo-title: 비디오 보기 숨기기
title: 비디오 보기 숨기기
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 비디오 보기 숨기기{#hide-a-video-view}

비디오를 재생하는 데 MediaPlayer 보기가 사용된 후 TV SDK 메서드를 사용하거나 수동으로 표시하여 숨길 수 있습니다.

비디오를 지우거나 디스플레이에서 이동하려면 먼저 비디오를 일시 중지해야 합니다.
* 옵션 1:비디오 프레임을 `MediaPlayer.clearVideo`&#x200B;으로 지우고 나중에 프레임을 바꿉니다.
   * 숨길 비디오를 일시 중지합니다.
   * `MediaPlayer.clearVideo`을(를) 호출하여 표시된 비디오 프레임을 제거합니다.
   * 다시 재생할 수 있도록 `MediaPlayer`을 다시 설정하려면 `replaceCurrentResource` 또는 `replaceCurrentItem`를 호출합니다.
* 옵션 2:`MediaPlayer` 보기를 화면에서 이동하여 나중에 교체하지 않고 다시 이동합니다.
   * 숨길 비디오를 일시 중지합니다.
   * 보기를 스테이지 밖으로 이동합니다. 예:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 비디오를 다시 표시하려면 보기를 스테이지로 다시 이동합니다.
