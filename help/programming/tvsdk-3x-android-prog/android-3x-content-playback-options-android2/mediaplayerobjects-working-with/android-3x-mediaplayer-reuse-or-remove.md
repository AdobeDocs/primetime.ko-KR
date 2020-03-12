---
description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-title: MediaPlayer 인스턴스 재사용 또는 제거
title: MediaPlayer 인스턴스 재사용 또는 제거
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# MediaPlayer 인스턴스 재사용 또는 제거 {#reuse-or-remove-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

## MediaPlayer 인스턴스 재설정 또는 재사용 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

인스턴스를 재설정하면 에 정의된 대로 `MediaPlayer` 초기화되지 않은 IDLE 상태로 반환됩니다 `MediaPlayerStatus`.

이 작업은 다음 경우에 유용합니다.

* 인스턴스를 재사용하려고 하지만 새(비디오 컨텐츠) `MediaPlayer` `MediaResource` 를 로드하고 이전 인스턴스를 교체해야 합니다.

   재설정을 사용하면 리소스를 해제하거나 다시 만들고 리소스를 다시 할당해야 하는 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 `MediaPlayer`수 있습니다.

* ERROR `MediaPlayer` 상태이고 이 상태를 지워야 하는 경우

   >[!IMPORTANT]
   >
   >ERROR 상태에서 복구할 수 있는 유일한 방법입니다.

   1. 인스턴스를 초기화되지 `reset` 않은 상태로 반환하려면 `MediaPlayer` 다음을 호출합니다.

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 다른 `MediaPlayer.replaceCurrentResource()` 항목을 로드하는 데 `MediaResource`사용합니다.

      >[!NOTE]
      >
      >오류를 지우려면 동일한 항목을 `MediaResource`로드합니다.

   1. 상태 `STATUS_CHANGED` 이벤트 콜백을 받으면 `PREPARED` 재생을 시작합니다.

## MediaPlayer 인스턴스 및 리소스 릴리스 {#section_13A0914AFF784943ABC343F7EB249C4E}

더 이상 필요하지 않은 `MediaPlayer` 인스턴스와 리소스를 해제해야 합니다 `MediaResource`.

개체를 놓으면 `MediaPlayer` 이 개체와 관련된 기본 하드웨어 리소스가 `MediaPlayer` 할당 해제됩니다.

다음은 `MediaPlayer`다음과 같은 경우에 릴리스해야 하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 미칠 수 있습니다.
* 불필요한 `MediaPlayer` 개체를 인스턴스화하면 모바일 장치에 대한 배터리 사용량이 계속 늘어날 수 있습니다.
* 한 장치에서 동일한 비디오 코덱의 여러 인스턴스가 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

* 를 `MediaPlayer`해제합니다.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 `MediaPlayer` 해제된 후 호출되면 `MediaPlayerException` throw됩니다.