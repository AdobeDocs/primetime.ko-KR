---
seo-title: 롤백 감지
title: 롤백 감지
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 롤백 감지 {#rollback-detection}

Adobe Access를 구현하면 클라이언트에서 상태를 유지해야 하는 비즈니스 규칙(예: 재생 창 간격)을 사용하는 경우 서버가 롤백 카운터를 추적하고 AIR 또는 SWF를 사용하여 나열을 제한하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에 따라 서버로 전송됩니다. Adobe Access 구현에 롤백 카운터가 필요하지 않은 경우 무시될 수 있습니다. 그렇지 않은 경우, 서버가 데이터베이스에 현재 카운터 값 `MachineToken.getMachineId().getUniqueId()`과 함께 사용하여 가져온 임의의 컴퓨터 ID를 저장하는 것이 좋습니다. 롤백 카운터의 증분 및 추적에 대한 자세한 내용은 *Adobe Access API 참조* 및 컨텐츠 보호를 위해 Adobe Access SDK 사용 *에서* ClientState 검색 *을*&#x200B;참조하십시오.
