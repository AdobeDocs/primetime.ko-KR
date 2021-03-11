---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
title: 볼륨 제어 제공
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 RELEASED 또는 ERROR를 제외한 이 명령에 대해 유효한 상태가 될 때까지 기다립니다.
1. `MediaPlayer` 인스턴스에서 `setVolume`을 호출하여 오디오 볼륨을 설정합니다.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서 0은 묵음이고 100은 최대 볼륨입니다.

