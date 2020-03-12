---
seo-title: 재생 보호
title: 재생 보호
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 재생 보호{#replay-protection}

재생 보호 기능을 사용하면 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 야기할 수 있습니다( *서비스 거부* 공격은 공격자의 시도로서 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 합니다). 예를 들어 롤백 카운터를 사용하는 재생 공격을 사용하여 DRM 클라이언트가 해당 상태를 롤백하고 있다고 판단하여 계정이 일시 중단되도록 라이센스 서버를 &quot;트릭&quot;할 수 있습니다.

재생 보호에 대한 자세한 내용은 Adobe Access `AbstractRequestMessage.getMessageId()` API *Reference를 참조하십시오*.
