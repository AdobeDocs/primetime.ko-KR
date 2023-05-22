---
description: 재생 보호는 공격자가 라이선스 요청 메시지를 재생하지 못하도록 하여 클라이언트에 대한 서비스 거부(DoS) 공격을 야기할 수 있습니다.
title: 재생 보호
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 재생 보호{#replay-protection}

재생 보호는 공격자가 라이선스 요청 메시지를 재생하지 못하도록 하여 클라이언트에 대한 서비스 거부(DoS) 공격을 야기할 수 있습니다.

DoS 공격은 공격자가 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 시도하는 것입니다. 예를 들어 롤백 카운터를 사용하는 재생 공격은 DRM 클라이언트가 상태를 롤백했다고 생각하도록 라이선스 서버를 &quot;트릭&quot;하는 데 사용할 수 있으며, 이로 인해 계정이 일시 중단됩니다.

재생 보호에 대한 자세한 내용은 다음을 참조하십시오. [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
