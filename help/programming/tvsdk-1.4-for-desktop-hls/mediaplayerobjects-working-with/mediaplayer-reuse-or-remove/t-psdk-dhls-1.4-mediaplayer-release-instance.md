---
description: MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.
seo-description: MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.
seo-title: MediaPlayer 인스턴스 및 리소스 릴리스
title: MediaPlayer 인스턴스 및 리소스 릴리스
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# MediaPlayer 인스턴스 및 리소스 릴리스{#release-a-mediaplayer-instance-and-resources}

MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.

개체를 놓으면 `MediaPlayer` 이 개체와 관련된 기본 하드웨어 리소스가 `MediaPlayer` 할당 해제됩니다.

다음은 `MediaPlayer`다음과 같은 경우에 릴리스해야 하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 미칠 수 있습니다.
* 한 장치에서 동일한 비디오 코덱의 여러 인스턴스가 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

1. 를 `MediaPlayer`해제합니다.

   ```
   function release():void;
   ```

인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 `MediaPlayer` 해제된 후 호출되면 `IllegalStateException` throw됩니다.