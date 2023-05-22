---
description: 'Adobe Primetime Adobe DRM 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버에서 롤백 카운터를 추적하고 AIR 또는 SWF 허용 목록을 사용하는 것이 좋습니다.'
title: 롤백 감지
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 롤백 감지 {#rollback-detection}

Adobe Primetime Adobe DRM 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버에서 롤백 카운터를 추적하고 AIR 또는 SWF 허용 목록을 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Primetime DRM 구현에서 롤백 카운터가 필요하지 않은 경우 무시할 수 있습니다. Adobe 그렇지 않으면 서버에서 를 사용하여 가져온 임의의 컴퓨터 ID를 저장하는 것이 좋습니다. [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())및 데이터베이스의 현재 카운터 값입니다.

롤백 카운터를 증가시키고 추적하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 및 롤백 감지입니다.