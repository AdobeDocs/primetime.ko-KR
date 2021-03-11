---
title: 재생 보호
description: 재생 보호
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 보호 재생{#replay-protection}

재생 보호의 경우 메시지 ID가 최근에 `RequestMessageBase.getMessageId()`에 전화하여 표시되었는지 여부를 확인하는 것이 신중할 수 있습니다. 이러한 경우 침입자가 요청을 다시 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재실행 시도를 탐지하기 위해 서버는 최근에 본 메시지 ID 목록을 저장하고 캐시된 목록에 대해 들어오는 각 요청을 확인할 수 있습니다. 메시지 식별자를 저장할 시간을 제한하려면 `HandlerConfiguration.setTimestampTolerance()`을(를) 호출하십시오. 이 속성이 설정되면 SDK는 지정된 시간(초) 이상의 타임스탬프를 포함하는 요청을 거부합니다.
