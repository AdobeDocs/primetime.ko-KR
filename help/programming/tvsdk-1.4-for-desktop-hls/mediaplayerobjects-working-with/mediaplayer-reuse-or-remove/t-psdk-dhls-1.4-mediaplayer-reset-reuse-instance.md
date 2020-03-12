---
description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.
seo-description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.
seo-title: MediaPlayer 인스턴스 재설정 또는 재사용
title: MediaPlayer 인스턴스 재설정 또는 재사용
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97

---


# MediaPlayer 인스턴스 재설정 또는 재사용{#reset-or-reuse-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 IDLE 상태로 반환됩니다.

이 작업은 다음 경우에 유용합니다.

* 인스턴스를 재사용하려고 하지만 새(비디오 컨텐츠) `MediaPlayer` `MediaResource` 를 로드하고 이전 인스턴스를 교체해야 합니다.

   재설정을 사용하면 리소스를 해제하거나 다시 만들고 리소스를 다시 할당해야 하는 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 `MediaPlayer`수 있습니다. 이 `replaceCurrentItem` 및 `replaceCurrentResource` 메서드는 reset 메서드를 호출하지 않고도 이러한 단계를 자동으로 수행합니다.

* ERROR `MediaPlayer` 상태가 있고 지워져야 하는 경우

   >[!IMPORTANT]
   >
   >ERROR 상태에서 복구할 수 있는 유일한 방법입니다.

1. 인스턴스를 초기화되지 `reset` 않은 상태로 `MediaPlayer` 반환하려면 다음을 호출합니다.

   ```
   function reset():void; 
   ```

1. 또는 를 사용하여 `MediaPlayer.replaceCurrentItem` 다른 `MediaPlayer.replaceCurrentResource` `MediaResource`항목을 로드합니다.

   >[!TIP]
   >
   >오류를 지우려면 동일한 항목을 `MediaResource`로드합니다.

1. 상태가 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 표시된 `PREPARED` 경우 재생을 시작합니다.
