---
description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.
seo-description: MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.
seo-title: MediaPlayer 인스턴스 재설정 또는 재사용
title: MediaPlayer 인스턴스 재설정 또는 재사용
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# MediaPlayer 인스턴스 재설정 또는 재사용{#reset-or-reuse-a-mediaplayer-instance}

더 이상 필요하지 않은 MediaPlayer 인스턴스를 재설정, 재사용 또는 해제할 수 있습니다.

MediaPlayer 인스턴스를 재설정하면 MediaPlayerStatus에 정의된 대로 초기화되지 않은 유휴 상태로 반환됩니다.

이 작업은 다음 경우에 유용합니다.

* `MediaPlayer` 인스턴스를 재사용하려는 경우 새 `MediaResource`(비디오 컨텐츠)을 로드하고 이전 인스턴스를 바꿔야 합니다.

   재설정을 사용하면 리소스를 해제하거나 `MediaPlayer`을(를) 다시 만들고 리소스를 다시 할당하는 등의 오버헤드 없이 `MediaPlayer` 인스턴스를 재사용할 수 있습니다. Reset 메서드를 호출할 필요 없이 `replaceCurrentItem` 및 `replaceCurrentResource` 메서드는 자동으로 이러한 단계를 수행합니다.

* `MediaPlayer`에 ERROR 상태가 있고 이 상태를 지워야 하는 경우

   >[!IMPORTANT]
   >
   >이 방법만이 ERROR 상태로부터 복구할 수 있습니다.

1. `reset`을(를) 호출하여 `MediaPlayer` 인스턴스를 초기화되지 않은 상태로 되돌립니다.

   ```
   function reset():void; 
   ```

1. `MediaPlayer.replaceCurrentItem` 또는 `MediaPlayer.replaceCurrentResource`을 사용하여 다른 `MediaResource`를 로드합니다.

   >[!TIP]
   >
   >오류를 지우려면 동일한 `MediaResource`을(를) 로드하십시오.

1. `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 상태가 `PREPARED`인 경우 재생을 시작합니다.
