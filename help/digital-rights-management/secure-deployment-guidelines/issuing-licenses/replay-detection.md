---
description: 재생 보호 기능을 사용하면 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 할 수 있습니다.
title: 재생 보호
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 보호 재생{#replay-protection}

재생 보호 기능을 사용하면 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 할 수 있습니다.

DoS 공격은 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 하기 위해 침입자가 시도하는 것입니다. 예를 들어, 롤백 카운터를 사용하는 재생 공격을 사용하여 DRM 클라이언트가 해당 상태를 롤백하여 계정을 일시 중단하도록 생각하게 하려면 라이센스 서버를 &quot;트릭&quot;할 수 있습니다.

재생 보호에 대한 자세한 내용은 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())를 참조하십시오.
