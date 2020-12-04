---
description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-description: 더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.
seo-title: MediaPlayer 인스턴스 재사용 또는 제거
title: MediaPlayer 인스턴스 재사용 또는 제거
uuid: da7b3468-3f0f-4025-927b-d47764a053af
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# MediaPlayer 인스턴스 {#reuse-or-remove-a-mediaplayer-instance} 재사용 또는 제거

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

## MediaPlayer 인스턴스 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9} 재설정 또는 재사용

`MediaPlayer` 인스턴스를 재설정하면 `MediaPlayerStatus`에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.

* `MediaPlayer` 인스턴스를 재사용하려는 경우 새 `MediaResource`(비디오 컨텐츠)을 로드하고 이전 인스턴스를 바꿔야 합니다.

   재설정을 사용하면 리소스를 해제하거나 `MediaPlayer`을(를) 다시 만들고 리소스를 다시 할당하는 등의 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 수 있습니다.

* `MediaPlayer`이(가) ERROR 상태이므로 이 상태를 지워야 합니다.

   >[!IMPORTANT]
   >
   >이 방법만이 ERROR 상태로부터 복구할 수 있습니다.

   1. `reset`을(를) 호출하여 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 되돌립니다.

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. `MediaPlayer.replaceCurrentResource()`을(를) 사용하여 다른 `MediaResource`을(를) 로드합니다.

      >[!NOTE]
      >
      >오류를 지우려면 동일한 `MediaResource`을(를) 로드하십시오.

   1. `STATUS_CHANGED` 이벤트 콜백을 수신하면 재생을 시작합니다.`PREPARED`

## MediaPlayer 인스턴스 및 리소스 {#section_13A0914AFF784943ABC343F7EB249C4E} 해제

`MediaResource`이(가) 더 이상 필요하지 않은 경우 `MediaPlayer` 인스턴스와 리소스를 해제해야 합니다.

`MediaPlayer` 개체를 놓으면 이 `MediaPlayer` 개체와 관련된 기본 하드웨어 리소스가 할당 해제됩니다.

다음은 `MediaPlayer`을(를) 해제해야 하는 몇 가지 이유입니다.

* 불필요한 리소스를 보유하는 것은 성능에 영향을 줄 수 있습니다.
* 불필요한 `MediaPlayer` 개체를 인스턴스화하면 모바일 장치에 대한 지속적인 배터리 소비로 이어질 수 있습니다.
* 한 장치에서 동일한 비디오 코덱의 여러 인스턴스가 지원되지 않는 경우 다른 응용 프로그램에서 재생 오류가 발생할 수 있습니다.

* `MediaPlayer`을(를) 해제합니다.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >`MediaPlayer` 인스턴스가 릴리스되면 더 이상 사용할 수 없습니다. `MediaPlayer` 인터페이스의 어떤 메서드도 실행 후 호출되면 `MediaPlayerException`이 발생합니다.