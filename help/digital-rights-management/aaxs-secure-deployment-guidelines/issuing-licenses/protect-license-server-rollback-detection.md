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

Adobe 액세스 구현에서 클라이언트가 상태를 유지 관리해야 하는 비즈니스 규칙을 사용하는 경우(예: 재생 창 간격), 서버가 롤백 카운터를 추적하고 AIR 또는 SWF 목록 허용 사용을 권장합니다.

롤백 카운터는 클라이언트의 대부분의 요청에 따라 서버로 전송됩니다. Adobe 액세스 구현에 롤백 카운터가 필요하지 않으면 무시될 수 있습니다. 그렇지 않은 경우 서버가 `MachineToken.getMachineId().getUniqueId()`을 사용하여 얻은 임의의 컴퓨터 ID와 현재 카운터 값을 데이터베이스에 저장하는 것이 좋습니다. 롤백 카운터의 증분 및 추적에 대한 자세한 내용은 *Adobe 액세스 API 참조* 및 *컨텐츠 보호를 위한 Adobe 액세스 SDK 사용*&#x200B;에서 *롤백 감지*&#x200B;의 ClientState를 참조하십시오.
