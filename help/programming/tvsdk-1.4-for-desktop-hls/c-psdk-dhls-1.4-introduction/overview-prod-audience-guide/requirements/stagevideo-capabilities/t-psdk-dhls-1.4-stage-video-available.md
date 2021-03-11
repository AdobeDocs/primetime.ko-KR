---
description: StageVideo를 사용할 수 없고 응용 프로그램에서 StageVideo를 사용하려고 하면 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 결정할 수 있습니다.
title: StageVideo 사용 가능 여부 확인
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---


# StageVideo를 사용할 수 있는지 확인{#check-whether-stagevideo-is-available}

StageVideo를 사용할 수 없고 응용 프로그램에서 StageVideo를 사용하려고 하면 TVSDK에서 오류가 발생하지 않습니다. 응용 프로그램은 StageVideoAvailabilityEvent를 수신하여 StageVideo를 사용할 수 있는지 여부를 결정할 수 있습니다.

Flash 15 이상에서 하드웨어 `StageVideo`을(를) 사용할 수 없는 경우 소프트웨어 `StageVideo`으로 돌아갑니다. Flash 14 이하 버전의 경우 `StageVideo`을(를) 사용할 수 있는지 여부를 결정할 수 있습니다. `StageVideo`을(를) 사용할 수 없는 경우 `StageVideoAvailabilityEvent`을(를) 사용하여 사용할 수 없는 이유를 파악할 수 있습니다.

1. `StageVideoAvailabilityEvent`을 들어 `StageVideo`을(를) 사용할 수 있는지 확인합니다.

   예:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. `StageVideo`을(를) 사용할 수 없는 경우 `flash.media.StageVideoAvailabilityReason`을(를) 확인하십시오.
