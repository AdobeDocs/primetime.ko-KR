---
description: TVSDK의 이벤트는 플레이어의 상태, 발생하는 오류, 재생을 시작하는 비디오와 같이 요청한 작업의 완료 또는 광고 완료와 같이 묵시적으로 발생하는 작업을 나타냅니다.
title: Primetime 플레이어 이벤트 수신
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 개요 {#implement-event-listeners-and-callbacks-overview}

이벤트 핸들러를 사용하면 TVSDK가 이벤트에 응답할 수 있습니다. 이벤트가 발생하면 TVSDK의 이벤트 메커니즘이 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 핸들러로 전달합니다.

Flash 런타임에서는 TVSDK가 일련의 사용자 지정 이벤트도 사용하고 정의하는 일반 이벤트 메커니즘을 제공합니다. 애플리케이션에 영향을 주는 TVSDK 이벤트에 대해 애플리케이션이 이벤트 리스너를 구현해야 합니다.

1. 애플리케이션이 수신해야 하는 이벤트를 결정합니다.

   * **필수 이벤트**: 모든 재생 이벤트를 수신합니다.

     >[!IMPORTANT]
     >
     >재생 이벤트 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 는 오류를 포함하여 플레이어 상태를 제공합니다. 모든 상태가 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**: 애플리케이션에 따라 선택 사항입니다.

     예를 들어 재생에 광고를 통합하는 경우 모두 수신 대기하십시오 `AdBreakPlaybackEvent` 및 `AdPlaybackEvent` 이벤트.

1. 각 이벤트에 대해 이벤트 리스너를 구현합니다.

   TVSDK는 이벤트 리스너 콜백에 매개 변수 값을 반환합니다. 이러한 값은 리스너에서 적절한 작업을 수행하는 데 사용할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   다음 `Event` 클래스는 모든 콜백 인터페이스를 나열합니다. 각 인터페이스는 해당 인터페이스에 대해 반환되는 매개 변수를 표시합니다.

   예:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 콜백 리스너를 `MediaPlayer` 을 사용한 개체 `MediaPlayer.addEventListener`.

   `MediaPlayer` 확장 `flash.events.IEventDispatcher`: Flash 플레이어 코어 파일의 일부이며 함수를 포함합니다 `addEventListener` 및 `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
