---
description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
title: MediaPlayer 인스턴스 재사용 또는 제거
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# MediaPlayer 인스턴스 {#reuse-or-remove-a-mediaplayer-instance} 재사용 또는 제거

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

## MediaPlayer 인스턴스 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9} 재설정 또는 재사용

`MediaPlayer` 인스턴스를 재설정하면 `MediaPlayerStatus`에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.

이 작업은 다음 경우에 유용합니다.

* `MediaPlayer` 인스턴스를 재사용하려고 하지만 새 `MediaResource`(비디오 컨텐츠)을 로드하고 이전 인스턴스를 바꿔야 합니다.

   재설정을 사용하면 리소스 해제, `MediaPlayer` 다시 만들기 및 리소스 재할당에 대한 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 수 있습니다.

* `MediaPlayer`이(가) ERROR 상태이므로 삭제해야 하는 경우

   >[!IMPORTANT]
   >
   >ERROR 상태로부터 복구하는 유일한 방법입니다.

   1. `reset`을(를) 호출하여 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 되돌립니다.

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 다른 `MediaResource`을(를) 로드하려면 `MediaPlayer.replaceCurrentResource()`을 사용합니다.

      >[!NOTE]
      >
      >오류를 지우려면 동일한 `MediaResource`을(를) 로드합니다.

   1. `PREPARED` 상태로 `STATUS_CHANGED` 이벤트 콜백을 받으면 재생을 시작합니다.

## MediaPlayer 인스턴스 및 리소스 {#section_13A0914AFF784943ABC343F7EB249C4E} 해제

`MediaResource`이(가) 더 이상 필요하지 않은 경우 `MediaPlayer` 인스턴스와 리소스를 해제해야 합니다.

`MediaPlayer` 개체를 놓으면 이 `MediaPlayer` 개체와 관련된 기본 하드웨어 리소스가 할당 해제됩니다.

다음은 `MediaPlayer`을(를) 해제하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 불필요한 `MediaPlayer` 개체를 인스턴스화하면 모바일 장치에 대한 지속적인 배터리 소비로 이어질 수 있습니다.
* 인스턴스가 여러 개인 경우
동일한 비디오-코덱의 s는 장치에서 지원되지 않으므로 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

* `MediaPlayer`을(를) 해제합니다.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >`MediaPlayer` 인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 실행 후 호출되면 `MediaPlayerException`이 발생합니다.