---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-title: 볼륨 제어 제공
title: 볼륨 제어 제공
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 볼륨 제어 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. 인스턴스가 이 명령에 대해 유효한 상태가 될 때까지 `MediaPlayer` 기다립니다.

   RELEASED 또는 ERROR를 제외한 모든 상태가 유효합니다.
1. 인스턴스에 볼륨 속성을 설정하여 오디오 볼륨을 설정합니다. `MediaPlayer`

   ```js
   player.volume = ...
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서 0은 묵음이고 최대 볼륨입니다.

