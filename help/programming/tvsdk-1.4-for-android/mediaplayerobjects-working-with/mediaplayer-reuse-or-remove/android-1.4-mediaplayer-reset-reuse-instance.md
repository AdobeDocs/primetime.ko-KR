---
description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerState에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.
seo-description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerState에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.
seo-title: MediaPlayer 인스턴스 재설정 또는 재사용
title: MediaPlayer 인스턴스 재설정 또는 재사용
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer 인스턴스 재설정, 재사용 또는 제거 {#reset-or-reuse-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

MediaPlayer 인스턴스를 재설정하면 MediaPlayerState에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.

이 작업은 다음 경우에 유용합니다.

* 인스턴스를 재사용하려고 하지만 새(비디오 컨텐츠) `MediaPlayer` `MediaResource` 를 로드하고 이전 인스턴스를 교체해야 합니다.

   재설정을 사용하면 리소스를 해제하거나 다시 만들고 리소스를 다시 할당해야 하는 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 `MediaPlayer`수 있습니다.

* ERROR `MediaPlayer` 상태에 있고 이 상태를 지워야 하는 경우

   >[!IMPORTANT]
   >
   >ERROR 상태에서 복구하는 유일한 방법입니다.

1. 인스턴스를 초기화되지 `reset` 않은 상태로 `MediaPlayer` 반환하려면 다음을 호출합니다.

   ```java
   void reset() throws IllegalStateException; 
   ```

1. 다른 `MediaPlayer.replaceCurrentResource` 항목을 로드하는 데 `MediaResource`사용합니다.

   >[!TIP]
   >
   >오류를 지우려면 동일한 항목을 `MediaResource`로드합니다.

1. 준비된 상태로 `STATUS_CHANGED` 이벤트 콜백을 받으면 재생을 시작합니다.

## MediaPlayer 인스턴스 및 리소스 릴리스{#release-a-mediaplayer-instance-and-resources}

MediaResource가 더 이상 필요하지 않은 경우 MediaPlayer 인스턴스 및 리소스를 해제해야 합니다.

개체를 놓으면 `MediaPlayer` 이 개체와 관련된 기본 하드웨어 리소스가 `MediaPlayer` 할당 해제됩니다.

다음은 MediaPlayer를 릴리스하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 미칠 수 있습니다.
* 불필요한 `MediaPlayer` 개체를 방치하면 모바일 장치의 배터리 사용량이 계속 늘어날 수 있습니다.
* 한 장치에서 동일한 비디오 코덱의 여러 인스턴스가 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

1. 를 `MediaPlayer`해제합니다.

   ```java
   void release() throws IllegalStateException;
   ```

인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 `MediaPlayer` 해제된 후 호출되면 `IllegalStateException` throw됩니다.