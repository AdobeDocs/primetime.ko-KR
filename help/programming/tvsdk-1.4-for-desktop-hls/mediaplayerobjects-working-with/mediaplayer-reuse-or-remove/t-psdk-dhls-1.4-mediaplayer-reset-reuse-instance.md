---
description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 IDLE 상태로 돌아갑니다.
title: MediaPlayer 인스턴스 재설정 또는 재사용
exl-id: e06a0052-ce0a-4a6c-8ebc-0666b109cf07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# MediaPlayer 인스턴스 재설정 또는 재사용{#reset-or-reuse-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 릴리스할 수 있습니다.

MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 IDLE 상태로 돌아갑니다.

이 작업은 다음과 같은 경우에 유용합니다.

* 을(를) 재사용합니다. `MediaPlayer` 인스턴스를 새로 로드해야 함 `MediaResource` (비디오 콘텐츠) 및 이전 인스턴스를 바꿉니다.

   재설정하면 를 재사용할 수 있습니다. `MediaPlayer` 리소스 해제 오버헤드가 없는 인스턴스, 다시 만들기 `MediaPlayer`및 리소스를 재할당합니다. 다음 `replaceCurrentItem` 및 `replaceCurrentResource` 메서드는 reset 메서드를 호출하지 않고도 이러한 단계를 자동으로 수행합니다.

* 다음의 경우 `MediaPlayer` 에 오류 상태가 있으며 삭제해야 합니다.

   >[!IMPORTANT]
   >
   >이것이 ERROR 상태에서 복구할 수 있는 유일한 방법입니다.

1. 호출 `reset` 반환 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 전환합니다.

   ```
   function reset():void; 
   ```

1. 사용 `MediaPlayer.replaceCurrentItem` 또는 `MediaPlayer.replaceCurrentResource` 다른 파일을 로드하려면 `MediaResource`.

   >[!TIP]
   >
   >오류를 지우려면 동일한 을 로드합니다 `MediaResource`.

1. 다음을 받을 때 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` (으)로 `PREPARED` 상태, 재생을 시작합니다.
