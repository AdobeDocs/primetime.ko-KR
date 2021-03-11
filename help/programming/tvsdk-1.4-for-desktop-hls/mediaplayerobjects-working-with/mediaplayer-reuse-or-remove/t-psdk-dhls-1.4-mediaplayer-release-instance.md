---
description: MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.
title: MediaPlayer 인스턴스 및 리소스 릴리스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# MediaPlayer 인스턴스 및 리소스 해제{#release-a-mediaplayer-instance-and-resources}

MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.

`MediaPlayer` 개체를 놓으면 이 `MediaPlayer` 개체와 관련된 기본 하드웨어 리소스가 할당 해제됩니다.

다음은 `MediaPlayer`을(를) 해제하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 동일한 비디오 코덱의 여러 인스턴스가 장치에서 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

1. `MediaPlayer`을(를) 해제합니다.

   ```
   function release():void;
   ```

`MediaPlayer` 인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 실행 후 호출되면 `IllegalStateException`이 발생합니다.