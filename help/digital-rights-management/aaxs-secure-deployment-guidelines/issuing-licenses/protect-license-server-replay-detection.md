---
title: 재생 보호
description: 재생 보호
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 재생 보호{#replay-protection}

재생 보호는 공격자가 라이선스 요청 메시지를 재생하여 클라이언트(A)에 대한 서비스 거부(DoS) 공격을 야기할 수 없도록 합니다 *서비스 거부* 공격은 공격자가 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 하는 시도입니다.) 예를 들어 롤백 카운터를 사용하는 리플레이 공격은 DRM 클라이언트가 상태를 롤백하고 있다고 생각하여 계정을 일시 중단하도록 라이선스 서버를 &quot;트릭&quot;하는 데 사용할 수 있습니다.

재생 보호에 대한 자세한 내용은 다음을 참조하십시오. `AbstractRequestMessage.getMessageId()` 다음 *Adobe 액세스 API 참조*.
