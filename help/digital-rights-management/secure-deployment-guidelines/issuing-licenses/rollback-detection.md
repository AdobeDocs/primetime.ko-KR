---
description: 'Adobe Primetime DRM의 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버가 롤백 카운터를 계속 추적하고 AIR 또는 SWF 화이트리스트를 사용하는 것이 좋습니다.'
seo-description: 'Adobe Primetime DRM의 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버가 롤백 카운터를 계속 추적하고 AIR 또는 SWF 화이트리스트를 사용하는 것이 좋습니다.'
seo-title: 롤백 감지
title: 롤백 감지
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# 롤백 감지 {#rollback-detection}

Adobe Primetime DRM의 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버가 롤백 카운터를 계속 추적하고 AIR 또는 SWF 화이트리스트를 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Primetime DRM의 구현에 롤백 카운터가 필요하지 않은 경우 무시될 수 있습니다. 그렇지 않으면 서버가 MachineToken.getUniqueId() [를 사용하여 얻은 무작위 컴퓨터 ID와](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())데이터베이스의 현재 카운터 값을 저장하는 것이 좋습니다.

롤백 카운터를 증분하고 추적하는 방법에 대한 자세한 내용은 ClientState [및](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) Rollback 검색을 참조하십시오.