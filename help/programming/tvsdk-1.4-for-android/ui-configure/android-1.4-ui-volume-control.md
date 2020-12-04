---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
seo-title: 볼륨 컨트롤 제공
title: 볼륨 컨트롤 제공
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 RELEASED 또는 ERROR를 제외한 이 명령에 대해 유효한 상태가 될 때까지 기다립니다.
1. 오디오 볼륨을 설정하려면 `MediaPlayer` 인스턴스의 `setVolume`을(를) 호출합니다.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서 0은 무음, 100은 최대 볼륨입니다.

