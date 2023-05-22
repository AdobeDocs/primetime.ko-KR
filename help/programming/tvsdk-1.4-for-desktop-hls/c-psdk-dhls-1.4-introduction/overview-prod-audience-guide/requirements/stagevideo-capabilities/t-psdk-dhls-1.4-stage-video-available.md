---
description: StageVideo를 사용할 수 없고 애플리케이션이 StageVideo를 사용하려고 하면 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 확인할 수 있습니다.
title: StageVideo 사용 가능 여부 확인
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# StageVideo 사용 가능 여부 확인{#check-whether-stagevideo-is-available}

StageVideo를 사용할 수 없고 애플리케이션이 StageVideo를 사용하려고 하면 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 확인할 수 있습니다.

Flash 15 이상부터(하드웨어가 `StageVideo` 을(를) 사용할 수 없습니다. 소프트웨어로 대체됩니다. `StageVideo`. Flash 14 및 이전 버전의 경우 `StageVideo` 을(를) 사용할 수 있습니다. If `StageVideo` 은(는) 사용할 수 없으며 다음을 사용할 수 있습니다. `StageVideoAvailabilityEvent` 사용할 수 없는 이유를 이해합니다.

1. 잘 들어 `StageVideoAvailabilityEvent` 여부를 결정하다 `StageVideo` 을(를) 사용할 수 있습니다.

   예:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. If `StageVideo` 을(를) 사용할 수 없습니다. 확인 `flash.media.StageVideoAvailabilityReason`.
