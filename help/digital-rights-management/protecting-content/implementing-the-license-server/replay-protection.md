---
title: 재생 보호
description: 재생 보호
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 재생 보호{#replay-protection}

재생 보호의 경우 를 호출하여 메시지 식별자가 최근에 표시되었는지 확인할 수 있습니다. `RequestMessageBase.getMessageId()`. 그런 경우 공격자가 요청을 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재생 시도를 검출하기 위해, 서버는 최근에 본 메시지 ID의 목록을 저장하고, 캐싱된 목록에 대해 각각의 수신 요청을 검사할 수 있다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 을 호출하십시오. `HandlerConfiguration.setTimestampTolerance()`. 이 속성이 설정되면 SDK는 지정된 서버 시간(초) 이상 동안 타임스탬프를 전달하는 모든 요청을 거부합니다.
