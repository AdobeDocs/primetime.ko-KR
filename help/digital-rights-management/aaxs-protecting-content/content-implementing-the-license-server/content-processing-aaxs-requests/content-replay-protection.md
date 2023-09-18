---
title: 재생 보호
description: 재생 보호
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 재생 보호{#replay-protection}

재생 보호를 위해 호출을 통해 메시지 식별자가 최근에 표시되었는지 확인하는 것이 신중할 수 있습니다 `RequestMessageBase.getMessageId()`. 그런 경우 공격자가 요청을 재생하려고 할 수 있으며 이는 거부되어야 합니다. 재생 시도를 검출하기 위해, 서버는 최근에 본 메시지 ID의 목록을 저장하고, 캐싱된 목록에 대해 각각의 수신 요청을 검사할 수 있다. 메시지 식별자를 저장해야 하는 시간을 제한하려면 을 호출하십시오. `HandlerConfiguration.setTimestampTolerance()`. 이 속성이 설정되면 SDK는 지정된 시간(초) 이상 서버 시간에 타임스탬프를 전달하는 모든 요청을 거부합니다.
