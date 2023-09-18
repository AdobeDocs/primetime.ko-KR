---
description: 사용자 인터페이스 컨트롤을 설정하여 비디오의 볼륨을 조정할 수 있습니다.
title: 볼륨 컨트롤 제공
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 볼륨 컨트롤 제공 {#provide-volume-control}

사용자 인터페이스 컨트롤을 설정하여 비디오의 볼륨을 조정할 수 있습니다.

1. 볼륨 컨트롤 인터페이스 요소의 콜백 루틴에서 플레이어가 이 명령에 대해 올바른 상태인지 확인합니다.

   >[!TIP]
   >
   >릴리즈됨 을 제외한 모든 상태가 유효합니다.

1. 호출 `setVolume` 오디오 볼륨을 설정합니다.

   예:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서, `0` 침묵이며 `1` 는 최대 볼륨입니다.
