---
description: MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 릴리스해야 합니다.
title: MediaPlayer 인스턴스 및 리소스 릴리스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# MediaPlayer 인스턴스 및 리소스 릴리스{#release-a-mediaplayer-instance-and-resources}

MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 릴리스해야 합니다.

를 릴리스할 때 `MediaPlayer` 개체와 관련된 기본 하드웨어 리소스 `MediaPlayer` 개체가 할당 해제되었습니다.

다음은 를 릴리스해야 하는 몇 가지 이유입니다. `MediaPlayer`:

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 동일한 비디오 코덱의 여러 인스턴스가 장치에서 지원되지 않는 경우 다른 응용 프로그램에 대해 재생 오류가 발생할 수 있습니다.

1. 릴리스 `MediaPlayer`.

   ```
   function release():void;
   ```

다음 이후 `MediaPlayer` 인스턴스가 릴리스되었으므로 더 이상 사용할 수 없습니다. 다음 방법 중 하나라도 `MediaPlayer` 인터페이스는 릴리스된 후에 호출됩니다. `IllegalStateException` 이 throw됩니다.
