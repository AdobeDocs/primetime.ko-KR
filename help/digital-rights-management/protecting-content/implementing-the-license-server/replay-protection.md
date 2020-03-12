---
seo-title: 재생 보호
title: 재생 보호
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 재생 보호{#replay-protection}

재생 보호를 위해, 전화를 통해 메시지 식별자가 최근에 표시되었는지 확인할 수 `RequestMessageBase.getMessageId()`있습니다. 이러한 경우, 침입자가 요청을 다시 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재생 시도를 감지하기 위해 서버는 최근에 본 메시지 ID 목록을 저장하고 캐시된 목록에 대해 들어오는 각 요청을 확인할 수 있습니다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 을 호출하십시오. `HandlerConfiguration.setTimestampTolerance()` 이 속성이 설정되면 SDK는 지정된 시간(초) 이상 타임스탬프를 포함하는 요청을 거부합니다.
