---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
title: 볼륨 컨트롤 제공
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 이 명령에 대해 올바른 상태가 될 때까지(RELEASED 또는 ERROR 제외) 기다립니다.
1. 호출 `setVolume` 다음에 있음 `MediaPlayer` 오디오 볼륨을 설정할 인스턴스입니다.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   볼륨의 값은 요청된 볼륨을 최대 볼륨의 비율로 표현하며, 여기서 0은 묵음, 100은 최대 볼륨입니다.
