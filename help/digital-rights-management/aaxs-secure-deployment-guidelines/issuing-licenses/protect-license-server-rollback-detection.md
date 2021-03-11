---
title: 롤백 감지
description: 롤백 감지
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 롤백 감지 {#rollback-detection}

Adobe Access 구현에서 클라이언트가 상태를 유지 유지해야 하는 비즈니스 규칙(예: 재생 창 간격)을 사용하는 경우 Adobe에서는 서버가 롤백 카운터를 추적하고 AIR 또는 SWF 목록 허가를 사용할 것을 권장합니다.

롤백 카운터는 클라이언트의 대부분의 요청에 따라 서버로 전송됩니다. Adobe 액세스를 구현할 때 롤백 카운터를 필요로 하지 않는 경우 이 카운터를 무시할 수 있습니다. 그렇지 않은 경우 Adobe은 서버가 `MachineToken.getMachineId().getUniqueId()`을 사용하여 얻은 임의의 컴퓨터 ID와 현재 카운터 값을 데이터베이스에 저장하는 것이 좋습니다. 롤백 카운터를 증가시키고 추적하는 방법에 대한 자세한 내용은 *컨텐트 보호를 위한 Adobe 액세스 SDK 사용*&#x200B;의 *Adobe 액세스 API 참조* 및 *롤백 감지*&#x200B;에서 ClientState를 참조하십시오.
