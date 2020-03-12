---
description: TVSDK의 이벤트는 플레이어의 상태, 발생한 오류, 재생을 시작하는 비디오와 같은 요청된 작업 완료 또는 광고 완료와 같이 암시적으로 발생하는 작업을 나타냅니다.
seo-description: TVSDK의 이벤트는 플레이어의 상태, 발생한 오류, 재생을 시작하는 비디오와 같은 요청된 작업 완료 또는 광고 완료와 같이 암시적으로 발생하는 작업을 나타냅니다.
seo-title: Primetime 플레이어 이벤트 수신
title: Primetime 플레이어 이벤트 수신
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 개요 {#implement-event-listeners-and-callbacks-overview}

이벤트 핸들러를 사용하면 TVSDK가 이벤트에 응답할 수 있습니다. 이벤트가 발생하면 TVSDK의 이벤트 메커니즘은 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 처리기에 전달합니다.

Flash 런타임은 TVSDK가 일련의 사용자 지정 이벤트를 사용하고 정의하는 일반적인 이벤트 메커니즘을 제공합니다. 응용 프로그램은 응용 프로그램에 영향을 주는 TVSDK 이벤트에 대한 이벤트 리스너를 구현해야 합니다.

비디오 분석에 대한 전체 이벤트 목록은 코어 비디오 [재생 추적을 참조하십시오](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. 응용 프로그램이 수신 대기해야 하는 이벤트를 결정합니다.

   * **필수 이벤트**:모든 재생 이벤트에 대한 의견 수렴

      >[!IMPORTANT]
      >
      >재생 이벤트는 오류를 포함하여 플레이어 상태를 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 제공합니다. 모든 주가 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**:애플리케이션에 따라 선택 사항입니다.

      예를 들어 재생에 광고를 포함시키는 경우 모든 `AdBreakPlaybackEvent` 이벤트와 `AdPlaybackEvent` 이벤트를 수신합니다.

1. 각 이벤트에 대한 이벤트 리스너를 구현합니다.

   TVSDK는 이벤트 리스너 콜백에 매개 변수 값을 반환합니다. 이러한 값은 리스너에서 적절한 작업을 수행하기 위해 사용할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   이 `Event` 클래스는 모든 콜백 인터페이스를 나열합니다. 각 인터페이스는 해당 인터페이스에 대해 반환되는 매개 변수를 표시합니다.

   예:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 를 사용하여 콜백 리스너를 `MediaPlayer` 개체에 등록합니다 `MediaPlayer.addEventListener`.

   `MediaPlayer` extends `flash.events.IEventDispatcher``addEventListener` `removeEventListener`를 참조하십시오.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


