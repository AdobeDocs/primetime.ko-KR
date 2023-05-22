---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
title: 볼륨 컨트롤 제공
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. 다음을 기다리십시오. `MediaPlayer` 인스턴스가 이 명령의 유효한 상태가 될 수 있습니다.

   RELEASED 또는 ERROR 를 제외한 모든 상태가 유효합니다.
1. 볼륨 속성을 설정합니다. `MediaPlayer` 오디오 볼륨을 설정할 인스턴스입니다.

   ```js
   player.volume = ...
   ```

   볼륨의 값은 요청된 볼륨을 최대 볼륨의 비율로 표현하며, 여기서 0은 묵음 상태이고 최대 볼륨입니다.
