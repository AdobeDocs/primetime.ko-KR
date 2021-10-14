---
description: 'TVSDK의 이벤트는 플레이어의 상태, 발생한 오류, 재생 시작 비디오와 같이 사용자가 요청한 작업 완료 또는 광고 완료와 같이 암시적으로 발생하는 작업(예: )을 나타냅니다.'
title: Primetime 플레이어 이벤트 수신
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 개요 {#implement-event-listeners-and-callbacks-overview}

이벤트 핸들러를 사용하면 TVSDK가 이벤트에 응답할 수 있습니다. 이벤트가 발생하면 TVSDK의 이벤트 메커니즘이 등록된 이벤트 핸들러를 호출하고 이벤트 정보를 핸들러에 전달합니다.

Flash 런타임은 TVSDK에서 일련의 사용자 지정 이벤트를 사용하고 정의하는 일반 이벤트 메커니즘을 제공합니다. 애플리케이션에 영향을 주는 TVSDK 이벤트에 대한 이벤트 리스너를 구현해야 합니다.

1. 응용 프로그램이 수신해야 하는 이벤트를 결정합니다.

   * **필수 이벤트**: 모든 재생 이벤트를 수신합니다.

      >[!IMPORTANT]
      >
      >재생 이벤트 `MediaPlayerStatusChangeEvent.STATUS_CHANGE`는 오류를 포함한 플레이어 상태를 제공합니다. 모든 상태는 플레이어의 다음 단계에 영향을 줄 수 있습니다.

   * **기타 이벤트**: 애플리케이션에 따라 선택 사항입니다.

      예를 들어 재생에 광고를 통합하는 경우 모든 `AdBreakPlaybackEvent` 및 `AdPlaybackEvent` 이벤트를 수신하십시오.

1. 각 이벤트에 대한 이벤트 리스너를 구현합니다.

   TVSDK는 이벤트-리스너 콜백에 매개 변수 값을 반환합니다. 이러한 값에서는 수신기에서 적절한 작업을 수행할 수 있는 이벤트에 대한 관련 정보를 제공합니다.

   `Event` 클래스는 모든 콜백 인터페이스를 나열합니다. 각 인터페이스에는 해당 인터페이스에 대해 반환되는 매개 변수가 표시됩니다.

   예:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. `MediaPlayer.addEventListener` 를 사용하여 `MediaPlayer` 개체에 콜백 리스너를 등록합니다.

   `MediaPlayer` 확장  `flash.events.IEventDispatcher`: Flash 플레이어 코어 파일의 일부이며 함수  `addEventListener` 및  `removeEventListener`를 포함합니다.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
