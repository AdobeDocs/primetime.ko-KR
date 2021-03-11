---
description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.
title: MediaPlayer 인스턴스 재설정 또는 재사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# MediaPlayer 인스턴스 재설정 또는 재사용{#reset-or-reuse-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.

이 작업은 다음 경우에 유용합니다.

* `MediaPlayer` 인스턴스를 재사용하려고 하지만 새 `MediaResource`(비디오 컨텐츠)을 로드하고 이전 인스턴스를 바꿔야 합니다.

   재설정을 사용하면 리소스 해제, `MediaPlayer` 다시 만들기 및 리소스 재할당에 대한 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 수 있습니다. 재설정 메서드를 호출하지 않고도 `replaceCurrentItem` 및 `replaceCurrentResource` 메서드는 자동으로 이러한 단계를 수행합니다.

* `MediaPlayer`에 ERROR 상태가 있고 이 상태를 지워야 할 때.

   >[!IMPORTANT]
   >
   >ERROR 상태로부터 복구하는 유일한 방법입니다.

1. `reset`을(를) 호출하여 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 되돌립니다.

   ```
   function reset():void; 
   ```

1. `MediaPlayer.replaceCurrentItem` 또는 `MediaPlayer.replaceCurrentResource`을 사용하여 다른 `MediaResource`를 로드합니다.

   >[!TIP]
   >
   >오류를 지우려면 동일한 `MediaResource`을(를) 로드합니다.

1. `PREPARED` 상태로 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED`을 받으면 재생을 시작합니다.
