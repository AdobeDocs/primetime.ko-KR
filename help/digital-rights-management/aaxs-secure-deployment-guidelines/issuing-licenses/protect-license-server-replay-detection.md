---
title: 재생 보호
description: 재생 보호
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 보호 재생{#replay-protection}

재생 보호 기능을 사용하면 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격(A *서비스 거부* 공격은 침입자가 해당 서비스를 합법적인 사용자가 사용하지 못하도록 하려는 시도입니다.) 예를 들어, 롤백 카운터를 사용한 재생 공격을 사용하여 라이센스 서버가 DRM 클라이언트가 해당 상태를 롤백하고 있으므로 계정이 일시 중단되도록 &quot;트릭&quot;할 수 있습니다.

재생 보호에 대한 자세한 내용은 `AbstractRequestMessage.getMessageId()` Adobe 액세스 API 참조&#x200B;*를 참조하십시오.*
