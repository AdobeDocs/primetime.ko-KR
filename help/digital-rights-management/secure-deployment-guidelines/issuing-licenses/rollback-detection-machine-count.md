---
description: 비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연결된 컴퓨터 ID를 저장해야 합니다.
title: 라이선스를 발급할 때 컴퓨터 개수
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 라이선스를 발급할 때 컴퓨터 개수 {#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연결된 컴퓨터 ID를 저장해야 합니다.

시스템 ID를 추적하는 가장 강력한 방법은 가 반환하는 값을 저장하는 것입니다. [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 데이터베이스의 메서드입니다. 새 요청이 수신되면 을 사용하여 요청의 시스템 ID를 알려진 시스템 ID와 비교합니다 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 는 ID를 비교하여 ID가 동일한 컴퓨터를 나타내는지 여부를 확인합니다. 이 비교는 적은 수의 컴퓨터 ID가 있는 경우에만 실용적입니다. 예를 들어, 사용자에게 도메인에 5개의 시스템이 허용된 경우, 데이터베이스에서 사용자의 사용자 이름과 연결된 시스템 ID를 검색하고 비교할 작은 데이터 세트를 얻을 수 있습니다.

익명 액세스를 허용하는 배포에 대해서는 이 비교가 실용적이지 않습니다. 이 경우, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 를 사용할 수 있습니다. 그러나 이 ID는 사용자가 Flash 및 Adobe AIR® 런타임 시 콘텐츠에 액세스하는 경우 동일할 수 없습니다.

>[!NOTE]
>
>사용자가 하드 드라이브를 다시 포맷하는 경우 ID가 유지되지 않습니다.