---
description: 사용자 인터페이스 컨트롤을 설정하여 비디오의 볼륨을 조정할 수 있습니다.
title: 볼륨 제어 제공
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 볼륨 컨트롤 {#provide-volume-control} 제공

사용자 인터페이스 컨트롤을 설정하여 비디오의 볼륨을 조정할 수 있습니다.

1. 볼륨 컨트롤 인터페이스 요소에 대한 콜백 루틴에서 플레이어가 이 명령에 대해 유효한 상태인지 확인하십시오.

   >[!TIP]
   >
   >RELEASED를 제외한 모든 상태가 유효합니다.

1. 오디오 볼륨을 설정하려면 `setVolume`을(를) 호출합니다.

   예:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서 `0`은 묵음이고 `1`은 최대 볼륨입니다.