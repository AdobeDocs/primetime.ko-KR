---
description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 릴리스할 수 있습니다.
title: MediaPlayer 인스턴스 재사용 또는 제거
exl-id: 8b84c7f1-713a-46b4-8eb7-d699a79e74b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# MediaPlayer 인스턴스 재사용 또는 제거 {#reuse-or-remove-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 릴리스할 수 있습니다.

## MediaPlayer 인스턴스 재설정 또는 재사용 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

을(를) 재설정할 때 `MediaPlayer` 인스턴스가에 정의된 대로 초기화되지 않은 IDLE 상태로 돌아갑니다. `MediaPlayerStatus`.

이 작업은 다음과 같은 경우에 유용합니다.

* 을(를) 재사용합니다. `MediaPlayer` 인스턴스를 새로 로드해야 함 `MediaResource` (비디오 콘텐츠) 및 이전 인스턴스를 바꿉니다.

   재설정하면 를 재사용할 수 있습니다. `MediaPlayer` 리소스 해제 오버헤드가 없는 인스턴스, 다시 만들기 `MediaPlayer`및 리소스를 재할당합니다.

* 다음의 경우 `MediaPlayer` 은(는) 오류 상태에 있으므로 지워야 합니다.

   >[!IMPORTANT]
   >
   >이것이 ERROR 상태에서 복구할 수 있는 유일한 방법입니다.

   1. 호출 `reset` 반환 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 전환합니다.

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 사용 `MediaPlayer.replaceCurrentResource()` 다른 파일을 로드하려면 `MediaResource`.

      >[!NOTE]
      >
      >오류를 지우려면 동일한 을 로드합니다 `MediaResource`.

   1. 다음을 받을 때 `STATUS_CHANGED` 다음을 포함하는 이벤트 콜백 `PREPARED` 상태, 재생을 시작합니다.

## MediaPlayer 인스턴스 및 리소스 릴리스 {#section_13A0914AFF784943ABC343F7EB249C4E}

을(를) 해제해야 합니다. `MediaPlayer` 인스턴스 및 리소스는 `MediaResource`.

를 릴리스할 때 `MediaPlayer` 개체와 관련된 기본 하드웨어 리소스 `MediaPlayer` 개체가 할당 해제되었습니다.

다음은 를 릴리스해야 하는 몇 가지 이유입니다. `MediaPlayer`:

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 불필요한 항목 남기기 `MediaPlayer` 인스턴스화된 개체는 모바일 장치에 대한 지속적인 배터리 소비를 초래할 수 있습니다.
* 동일한 비디오 코덱의 여러 인스턴스가 장치에서 지원되지 않는 경우 다른 응용 프로그램에 대해 재생 오류가 발생할 수 있습니다.

* 릴리스 `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >다음 이후 `MediaPlayer` 인스턴스가 릴리스되었으므로 더 이상 사용할 수 없습니다. 다음 방법 중 하나라도 `MediaPlayer` 인터페이스는 릴리스된 후에 호출됩니다. `MediaPlayerException` 이 throw됩니다.
