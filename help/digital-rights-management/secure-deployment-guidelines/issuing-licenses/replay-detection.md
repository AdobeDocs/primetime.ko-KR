---
description: 재생 보호 기능은 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 발생시킵니다.
seo-description: 재생 보호 기능은 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 발생시킵니다.
seo-title: 재생 보호
title: 재생 보호
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 재생 보호{#replay-protection}

재생 보호 기능은 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 발생시킵니다.

DoS 공격은 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 하기 위한 공격자의 시도입니다. 예를 들어 롤백 카운터를 사용하는 재생 공격을 사용하여 DRM 클라이언트가 상태를 롤백했다고 판단하여 계정 일시 중단을 발생시킬 수 있습니다.

재생 보호에 대한 자세한 내용은 AbstractRequestMessage.getMessageId() [ 를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())참조하십시오.
