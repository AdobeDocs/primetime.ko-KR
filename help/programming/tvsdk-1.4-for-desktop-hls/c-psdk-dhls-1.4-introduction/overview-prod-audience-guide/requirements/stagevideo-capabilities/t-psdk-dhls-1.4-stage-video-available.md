---
description: StageVideo를 사용할 수 없고 응용 프로그램에서 StageVideo를 사용하려고 할 경우 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 결정할 수 있습니다.
seo-description: StageVideo를 사용할 수 없고 응용 프로그램에서 StageVideo를 사용하려고 할 경우 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 결정할 수 있습니다.
seo-title: StageVideo 사용 가능 여부 확인
title: StageVideo 사용 가능 여부 확인
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo 사용 가능 여부 확인{#check-whether-stagevideo-is-available}

StageVideo를 사용할 수 없고 응용 프로그램에서 StageVideo를 사용하려고 할 경우 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 결정할 수 있습니다.

Flash 15 이상 버전에서 하드웨어를 사용할 수 `StageVideo` 없는 경우 소프트웨어로 돌아갑니다 `StageVideo`. Flash 14 및 이전 버전의 경우 사용 가능 여부를 결정할 수 `StageVideo` 있습니다. 사용할 수 `StageVideo` 없는 경우 사용할 수 없는 이유를 알 `StageVideoAvailabilityEvent` 수 있습니다.

1. 사용 `StageVideoAvailabilityEvent` 가능 여부를 확인할 수 `StageVideo` 있습니다.

   예:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 사용할 수 `StageVideo` 없는 경우 확인하십시오 `flash.media.StageVideoAvailabilityReason`.
