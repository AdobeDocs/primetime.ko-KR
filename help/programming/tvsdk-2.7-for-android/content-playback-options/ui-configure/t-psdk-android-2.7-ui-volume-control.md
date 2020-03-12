---
description: 사용자 인터페이스 컨트롤을 설정하여 비디오 볼륨을 조정할 수 있습니다.
seo-description: 사용자 인터페이스 컨트롤을 설정하여 비디오 볼륨을 조정할 수 있습니다.
seo-title: 볼륨 제어 제공
title: 볼륨 제어 제공
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 볼륨 제어 제공 {#provide-volume-control}

사용자 인터페이스 컨트롤을 설정하여 비디오 볼륨을 조정할 수 있습니다.

1. 볼륨 컨트롤 인터페이스 요소에 대한 콜백 루틴에서 플레이어가 이 명령에 대해 유효한 상태인지 확인하십시오.

   >[!TIP]
   >
   >RELEASED를 제외한 모든 상태는 유효합니다.

1. 오디오 볼륨을 `setVolume` 설정하려면 전화 걸기

   예:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. `0` 이 경우 볼륨을 최대화하지 않고 `1` 최대 볼륨입니다.

